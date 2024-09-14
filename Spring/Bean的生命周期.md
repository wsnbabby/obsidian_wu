
### BeanPostProcessor
> 容器级处理器，每个Bean初始化都会调用

### InitializingBean
> `InitializingBean` 是 Spring 提供的一个接口，定义了一个方法 `afterPropertiesSet()`，该方法会在`Bean`的所有属性被设置后（即依赖注入完成后）被调用。


### @PostConstruct
> 可以在任何方法上使用 `@PostConstruct` 注解，该方法会在`依赖注入`完成后立即执行，相比 `InitializingBean` 更加灵活。
> 与Spring无关、javax包