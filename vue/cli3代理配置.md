## cli3代理配置

在根目录新建一个vue.config.js文件
```js
module.exports = {
  // cli3 代理是从指定的target后面开始匹配的，不是任意位置；配置pathRewrite可以做替换
  devServer: {
    proxy: {
      '/api': {
        target: 'http://112.74.99.5:3000/web/api',
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
}

```

配置好之后,重启项目

使用
```js


  methods: {
    articleitemData () {
      this.$http.get('/api/article/' + this.$route.params.id).then(res => {
        console.log(res)
        if (res && res.data && res.data.length) {
          // alert(123)
          this.model = res.data[0]
        } else {
          this.$toast('没有数据哦')
        }
      }).catch(e => {
        this.$toast(e.message)
        console.dir(e, '5555')
      })
      // console.log(res.data)
    }
  }
```