

## 依赖包与源码分开打包

- pom.xml配置如下
```xml
<build>  
    <plugins>        <!-- 指定jdk版本，和指定编码 -->  
        <plugin>  
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-compiler-plugin</artifactId>  
            <configuration>                <source>${java.version}</source>  
                <target>${java.version}</target>  
                <encoding>UTF-8</encoding>  
            </configuration>        </plugin>        <!--拷贝依赖到jar外面的lib目录-->  
        <plugin>  
            <groupId>org.apache.maven.plugins</groupId>  
            <artifactId>maven-dependency-plugin</artifactId>  
            <executions>                <execution>                    <id>copy-dependencies</id>  
                    <phase>package</phase>  
                    <goals>                        <goal>copy-dependencies</goal>  
                    </goals>                    <configuration>                        <outputDirectory>${project.build.directory}/lib</outputDirectory>  
                        <excludeTransitive>false</excludeTransitive>  
                        <stripVersion>false</stripVersion>  
                        <includeScope>runtime</includeScope>  
                    </configuration>                </execution>            </executions>        </plugin>        <plugin>            <groupId>org.springframework.boot</groupId>  
            <artifactId>spring-boot-maven-plugin</artifactId>  
            <version>2.5.15</version>  
            <configuration>                <layout>ZIP</layout>  
                <includes>                    <include>                        <groupId>non-exists</groupId>  
                        <artifactId>non-exists</artifactId>  
                    </include>                </includes>            </configuration>            <executions>                <execution>                    <goals>                        <goal>repackage</goal>  
                    </goals>                </execution>            </executions>        </plugin>    </plugins>    <finalName>${project.artifactId}</finalName>  
</build>
```

- 启动参数如下：
```sh
java -jar -Dloader.path=./lib target.jar
```