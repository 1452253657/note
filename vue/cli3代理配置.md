## cli3代理配置

在根目录新建一个

#### vue.config.js文件

```js
module.exports = {
  // cli3 代理是从指定的target后面开始匹配的，不是任意位置；配置pathRewrite可以做替换
  devServer: {
    proxy: {
      '/api': {//名字任意取
        target: 'http://112.74.99.5:3000/web/api',//本地服务器
        changeOrigin: true,
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
}

```

#### 配置好之后,重启项目



使用
```


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




###例子

``` main.js 里面

在main.js里面
//axios.defaults.baseURL = 'http://localhost:3000'

Vue.prototype.$axios = axios

Vue.prototype.$api = Api

Vue.use(ElementUI);

Vue.config.productionTip = false



在配置api的文件 index.js里 ,在每个接口前都加上'/api'  (这里已经加上了)

export default {

  add: '/api/addUser',           //新增一条数据  必传name age

  del: '/api/deleteUser',        //根据id删除一条数据 必传 id    

  update: '/api/updateUser',      //根据id修改对应数据  必传id name age

  queryAll: '/api/queryAll',     // 查 

  detail: '/api/query',          // 获取详情

  queryName: '/api/queryName',   // 根据name查询列表 必传 name

  upload: '/api/upload',         //   上传文件

}

```



