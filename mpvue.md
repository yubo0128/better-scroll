## 页面跳转带返回按钮

```JavaScript
wx.navigateTo({
        url:'/pages/list/main'
      })
```

### 登陆

```JavaScript
 <button class="go" open-type="getUserInfo" @getuserinfo="getUserInfo">确定</button>


created () { 
       wx.getUserInfo({
          success: res =>{
            console.log(res,'登陆成功')
          },
          fail: ()=> {
            console.log('获取失败')
          }
        })
  }

methods:{
   getUserInfo(data) {
      console.log("获取成功")
      console.log(data)
    }  
}

```

### 使用组件

```javascript
//引入组件
import ListTmp from '../list_template/list_template.vue'
//注册组件
export default {
 components：{ListTmp}
}
//在html中使用组件
<ListTmp />
```

 

dispatch：含有异步操作，例如向后台提交数据，写法： this.$store.dispatch('mutations方法名',值)

commit：同步操作，写法：this.$store.commit('mutations方法名',值)