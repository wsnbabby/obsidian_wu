### META-INF/spring.factories

	仿照Java中的SPI扩展机制，由SpringFactoriesLoader类，实现了检索META-INF/spring.factories文件，并获取指定接口的配置的功能。
	格式：com.xxx.interface=com.xxx.classname，key为接口全类名，value为具体实现类

引用：https://blog.csdn.net/weixin_38972910/article/details/123632630


### /META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports
	注意，从spring boot2.7开始，慢慢不支持META-INF/spring.factories文件了
	sptring-boot-autoconfigure-2.7.0.jar