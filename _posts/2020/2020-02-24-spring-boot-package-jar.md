# spring-boot打可执行包的方式


## 插件1

```
<plugins>
        <plugin>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-maven-plugin</artifactId>
          <version>2.0.1.RELEASE</version>
          <configuration>
            <mainClass>com.sunpx.Application</mainClass>
          </configuration>
          <executions>
            <execution>
              <goals>
                <goal>repackage</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
```
mvn package spring-boot:repackage


