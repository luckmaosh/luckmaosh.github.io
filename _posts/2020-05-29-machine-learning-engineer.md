---
layout: post
title: 机器学习工程化（一）
date: 2020-05-29
categories: ai
tags: ai
---

## 神经网络的计算过程
神经网络结构如下图所示，最左边的是输入层，最右边的是输出层，中间是多个隐含层，隐含层和输出层的每个神经节点，都是由上一层节点乘以其权重累加得到，标上“+1”的圆圈为截距项b，对输入层外每个节点：Y=w0*x0+w1*x1+…+wn*xn+b，由此我们可以知道神经网络相当于一个多层逻辑回归的结构。


![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gf9bgr5mglj30dw07m75s.jpg)


算法计算过程：输入层开始，从左往右计算，逐层往前直到输出层产生结果。如果结果值和目标值有差距，再从右往左算，逐层向后计算每个节点的误差，并且调整每个节点的所有权重，反向到达输入层后，又重新向前计算，重复迭代以上步骤，直到所有权重参数收敛到一个合理值。

原文链接：https://blog.csdn.net/happytofly/article/details/80121851

所以这是一种监督学习的过程。

## 截距项



## 多层神经网络完整程序实现


train方法是程序的入口，构造函数初始化完数据之后，就可以调用train方法


```java
import java.util.Random;
public class BpDeep{
    public double[][] layer;//神经网络各层节点
    public double[][] layerErr;//神经网络各节点误差
    public double[][][] layer_weight;//各层节点权重
    public double[][][] layer_weight_delta;//各层节点权重动量
    public double mobp;//动量系数
    public double rate;//学习系数


    // 构造函数是初始化数据
    public BpDeep(int[] layernum, double rate, double mobp){
        this.mobp = mobp;
        this.rate = rate;
        layer = new double[layernum.length][];
        layerErr = new double[layernum.length][];
        layer_weight = new double[layernum.length][][];
        layer_weight_delta = new double[layernum.length][][];
        Random random = new Random();
        for(int l=0;l<layernum.length;l++){
            layer[l]=new double[layernum[l]];
            layerErr[l]=new double[layernum[l]];
            if(l+1<layernum.length){
                layer_weight[l]=new double[layernum[l]+1][layernum[l+1]];
                layer_weight_delta[l]=new double[layernum[l]+1][layernum[l+1]];
                for(int j=0;j<layernum[l]+1;j++)
                    for(int i=0;i<layernum[l+1];i++)
                        layer_weight[l][j][i]=random.nextDouble();//随机初始化权重
            }   
        }
    }
    //逐层向前计算输出
    public double[] computeOut(double[] in){
        for(int l=1;l<layer.length;l++){
            for(int j=0;j<layer[l].length;j++){
                double z=layer_weight[l-1][layer[l-1].length][j];
                for(int i=0;i<layer[l-1].length;i++){
                    layer[l-1][i]=l==1?in[i]:layer[l-1][i];
                    z+=layer_weight[l-1][i][j]*layer[l-1][i];
                }
                layer[l][j]=1/(1+Math.exp(-z));
            }
        }
        return layer[layer.length-1];
    }
    //逐层反向计算误差并修改权重
    public void updateWeight(double[] tar){
        int l=layer.length-1;
        for(int j=0;j<layerErr[l].length;j++)
            layerErr[l][j]=layer[l][j]*(1-layer[l][j])*(tar[j]-layer[l][j]);

        while(l-->0){
            for(int j=0;j<layerErr[l].length;j++){
                double z = 0.0;
                for(int i=0;i<layerErr[l+1].length;i++){
                    z=z+l>0?layerErr[l+1][i]*layer_weight[l][j][i]:0;
                    layer_weight_delta[l][j][i]= mobp*layer_weight_delta[l][j][i]+rate*layerErr[l+1][i]*layer[l][j];//隐含层动量调整
                    layer_weight[l][j][i]+=layer_weight_delta[l][j][i];//隐含层权重调整
                    if(j==layerErr[l].length-1){
                        layer_weight_delta[l][j+1][i]= mobp*layer_weight_delta[l][j+1][i]+rate*layerErr[l+1][i];//截距动量调整
                        layer_weight[l][j+1][i]+=layer_weight_delta[l][j+1][i];//截距权重调整
                    }
                }
                layerErr[l][j]=z*layer[l][j]*(1-layer[l][j]);//记录误差
            }
        }
    }


    //程序入库，先向前计算，然后更新
    public void train(double[] in, double[] tar){
        double[] out = computeOut(in);
        updateWeight(tar);
    }
}
```


## 反向计算过程

- 误差函数

神经网络的输出和结果有误差时，才会方向计算，调整各个神经元的权重。如何计算误差呢？一般采用平方型误差函数E，如下：

![](https://tva1.sinaimg.cn/large/007S8ZIlly1gf9bljosugj307002nq2w.jpg)


o是输出值，t是目标值，这个公式的含义是将多个输出项和目标值的误差平方累加起来，再除以2。


也就是误差函数。



[如何用70行Java代码实现深度神经网络算法 ](http://geek.csdn.net/news/detail/56086)
Lane N D, Bhattacharya S, Georgiev P, et al. An early resource characterization of deep learning on wearables, smartphones and internet-of-things devices[C]//Proceedings of the 2015 International Workshop on Internet of Things towards Applications. ACM, 2015: 7-12. 
[CNN(卷积神经网络)是什么？有入门简介或文章吗？—机器之心的回答](https://www.zhihu.com/question/52668301)
[怎样通俗易懂地解释卷积？—冯小帅的回答 ](https://www.zhihu.com/question/22298352/answer/35652690)

[反向计算的具体案例！ 非常详细 推荐看](https://zhuanlan.zhihu.com/p/23270674)