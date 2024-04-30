## 原理
> 减少请求次数，将多条请求命令合成一次请求通过管道发给redis server，再通过回调函数一次性接收多个命令的结果，减少网络IO次数，在高并发情况下可带来明显性能提升。注意的是，redis server是单线程，多个命令合成一次请求到达redis server依然还是顺序一个个执行的，仅仅只是减少了请求IO次数。


## RedisCallback和SessionCallBack
> 1.作用: 让RedisTemplate进行回调，通过他们可以在同一条连接中一次执行多个redis命令。
> 2.SessionCalback提供了良好的封装，优先使用它。
> 3.RedisCallback使用的是原生RedisConnection，用起来比较麻烦，可读性差，但原生api提供的功能比较齐全。


## pom依赖

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

```java
@Component
public class RedisTest {
 
    @Autowired
    RedisTemplate<String, Object> redisTemplate;
 
    @PostConstruct
    public void init() {
        test1();
    }
 
    public void test1() {
        List<Object> pipelinedResultList = redisTemplate.executePipelined(new SessionCallback<Object>() {
            @Override
            public <K, V> Object execute(RedisOperations<K, V> operations) throws DataAccessException {
                ValueOperations<String, Object> valueOperations = (ValueOperations<String, Object>) operations.opsForValue();
 
                valueOperations.set("yzh1", "hello world");
                valueOperations.set("yzh2", "redis");
 
                valueOperations.get("yzh1");
                valueOperations.get("yzh2");
 
                // 返回null即可，因为返回值会被管道的返回值覆盖，外层取不到这里的返回值
                return null;
            }
        });
        System.out.println("pipelinedResultList=" + pipelinedResultList);
    }
}
```

结果：
`pipelinedResultList=[true, true, hello world, redis]`