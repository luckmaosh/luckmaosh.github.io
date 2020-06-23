https://www.jianshu.com/p/ce85ced8ed99?utm_campaign=hugo&utm_medium=reader_share&utm_content=note

  2.经过上面设置后，错误信息变为如下：
org.springframework.web.util.NestedServletException: Handler dispatch failed; nested exception is java.lang.UnsatisfiedLinkError: /tmp/jna--851256601/jna5078348374504753050.tmp: ELF file's phentsize not the expected size
    at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1054)

           以为是so包的原因，很建demo 生成jar包测试没有问题，最好发现是我的spintboot默认把资源问题压缩了，需要排除掉到so文件压缩

           解决方案：在pom中把so文件过滤掉，如下设置



maven进行资源过滤的时候，只要过滤需要过滤的文件，一些二进制文件，比如https证书等，就不要参与资源过滤，否则打包后会破坏文件内容。

```xml
<resources>
	<!--排除ip.dat，不打包到classpath下，自然就不会过滤-->
	<resource>
		<directory>src/main/resources</directory>
		<filtering>true</filtering>
		<excludes>
			<exclude>ip.dat</exclude>
		</excludes>
	</resource>
	
	<!--将ip.dat打包到classpath下，但是不进行资源过滤-->
	<resource>
		<directory>src/main/resources</directory>
		<filtering>false</filtering>
		<includes>
			<include>ip.dat</include>
		</includes>
	</resource>
</resources>
```


Maven resource 中的<include>与<exclude>用于包含或排除某一文件目录下的文件是否是工程资源的。

若<include>与<exclude>划定的范围存在冲突，则以<exclude>配置为准。

多数情况下，使用<include>和<exclude>是为了配合<filtering>实现替换文件中的变量的需要。

例如：

在某一个工程中，src/main/resources目录下都是工程的资源文件，并不需要<include>和<exclude>再进行划定。

但如果需要对且仅对其中的jdbc.properties和mail.properties两个文件进行过滤，则需要借助<include>和<exclude>进行如下的配置：

```xml 
<resources>
<!-- Filter jdbc.properties & mail.properties.-->
<!-- NOTE: We don't filter applicationContext-*.xml -->
  <resource>
    <directory>src/main/resources</directory>
    <filtering>true</filtering>
    <includes>
      <include>jdbc.properties</include>
      <include>mail.properties</include>
    </includes>
  </resource>
  <!-- Include other files as resources files. -->
  <resource>
    <directory>src/main/resources</directory>
    <filtering>false</filtering>
    <excludes>
      <exclude>jdbc.properties</exclude>
      <exclude>mail.properties</exclude>
    </excludes>
  </resource>
</resources>
```

其中第一段<resource>配置声明：在src/main/resources目录下，仅jdbc.properties和mail.properties两个文件是资源文件，然后，这两个文件需要被过滤。而第二段<resource>配置声明：同样在src/main/resources目录下，除jdbc.properties和mail.properties两个文件外的其他文件也是资源文件，但是它们不会被过滤。