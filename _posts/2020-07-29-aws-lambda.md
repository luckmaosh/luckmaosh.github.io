# 亚马逊AWS Lambda

>现在，随着 Serverless 的深入人心，云厂商都在说，“我们在定义 Serverless”，而开发者都说”我们在做 Serverless“，用户都是“在用 Serverless",人人都在往 Serverless 体系上靠，或多或少的沾点边，使得整个社区欣欣向荣。

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gh9vy1zsikj30k00b9wev.jpg)


虽然大家都在都在说serverless，云厂商也在提供serverless，目前 Serverless 体系，首选的是 FaaS + BaaS 模型，使用了 FaaS。所谓FAAS就是Function as a service功能即服务，BAAS就是BaaS（后端即服务：Backend as a Service）

这些东西有什么用呢，在思考这个问题以前，我们要想清楚，这个东西能为业务解决什么问题。如果可以给业务落地提高效率，它就是银弹，否则就是花拳绣腿。

## AWS Lambda
AWS Lambda 是一项计算服务，使用时无需预配置或管理服务器即可运行代码。AWS Lambda 只在需要时执行代码并自动缩放。借助 AWS Lambda，几乎可以为任何类型的应用程序或后端服务运行代码，而且无需执行任何管理。现在 AWS Lambda 支持 Node.js、Java、C# 和 Python。


- 使用java开发函数
- 使用 Gradle 构建部署程序包
- 上传使用 Lambda API 上传部署程序包

```bash
~/my-function$ aws lambda update-function-code --function-name my-function --zip-file fileb://my-function.zip
{
    "FunctionName": "my-function",
    "FunctionArn": "arn:aws:lambda:us-east-2:123456789012:function:my-function",
    "Runtime": "java8",
    "Role": "arn:aws:iam::123456789012:role/lambda-role",
    "Handler": "example.Handler",
    "CodeSha256": "Qf0hMc1I2di6YFMi9aXm3JtGTmcDbjniEuiYonYptAk=",
    "Version": "$LATEST",
    "TracingConfig": {
        "Mode": "Active"
    },
    "RevisionId": "983ed1e3-ca8e-434b-8dc1-7d72ebadd83d",
    ...
}
```

- 示例代码

https://github.com/awsdocs/aws-lambda-developer-guide/tree/master/sample-apps/blank-java


- AWS Lambda 提供以下适用于 Java 函数的库：

com.amazonaws:aws-lambda-java-core（必需）– 定义处理程序方法接口和运行时传递给处理程序的上下文对象。如果您定义自己的输入类型，则这是您唯一需要的库。

com.amazonaws:aws-lambda-java-events – 来自调用 Lambda 函数的服务的事件的输入类型。

com.amazonaws:aws-lambda-java-log4j2 – Log4j 2 的 Appender 库，可用于将当前调用的请求 ID 添加到功能日志中。