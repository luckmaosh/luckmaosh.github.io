
>Learn once, write anywhere

React Native is an open-source mobile application framework created by Facebook.[

## 环境搭建
    
配置签名

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gfdo4wxi72j31600kudjw.jpg)


ios版本选择自己手机的版本

部署信息也选好


![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfdo6qppgqj312o0u079j.jpg)

点击编译

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfdo78d27rj31gc066tc9.jpg)


结果就报错了，提示这个语法只支持ios13

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfdo7wsbfaj31c10u0npd.jpg)


环境

npm install -g react-native-cli

## init project
expo init project

## start

cd project
yarn start


##  react-native
react-native init demo
cd demo
npx react-native run-ios

## 运行原理

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfogago4w3j30wm0fggn3.jpg)

从图中可以看到，我们整个的 RN 应用可以分为两层展示：

- JavaScript Code 层
- Native Code 层

也可以理解为所谓的应用层和底层。应用层通过 JavaScript 桥接层 与底层平台进行交互，获取底层平台的原生 APIs、UI 组件及一些自定义组件等。比如 Hello world 示例中引入的 AppRegistry API 和 Text 组件便是很好的说明。

这样的分层能够使应用层的开发变得简单、高效和跨平台，对于应用的稳定性、运行时的性能来说将和原生平台保持接近。

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gfogbpkth4j30wc0jkgn0.jpg)


## Redux 架构

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfogcvym6sj30to0gmgn1.jpg)


##  React Native 中 的 Flex 布局

在开发 RN 项目时，官方推荐使用的布局方式是 Flex 布局，因为 Flexbox 可以在不同屏幕尺寸上提供一致的布局结构，这也解决了跨平台布局呈现的问题


## 线上热更新

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gfoggtvorbj30iv0ekjs0.jpg)