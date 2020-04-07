
```
export default {
    data() {
        return {
            name: 'Joe'
        }
    },
    watch: {
        name: {
            handler: 'sayName',
            immediate: true
        }
    },
    methods: {
        sayName() {
            console.log(this.name)
        }
    }
}

```

## watch 
是在监听属性改变时才会触发（这里是监听name属性），有些时候，我们希望在组件创建后 watch 能够立即执行
可能想到的的方法就是在 create 生命周期中调用一次，但这样的写法不优雅，或许我们可以使用这样的方法


## methods
定义所有的方法

