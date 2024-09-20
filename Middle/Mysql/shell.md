
```shell
// 登录
mysql -u root -p


```



### nginx配置mysql转发

```nginx
stream {
    upstream sql {
	    # mysql实际部署的机器
        server 192.168.6.80:3306;   
    }
    server {
	   # 对外暴露端口 
       listen     3306;
       proxy_connect_timeout 10s;  
       proxy_timeout 10m;
       proxy_pass sql;
    }
}
```

