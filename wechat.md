# Wechat Mini Program

## 跳转
### 1.1 对标签绑定点击事件
```html
<text bindtap="clickme" data-nid="123" data-name="NAME">Click me.</text>
```

定义在page.js中的js函数
```js
Page({
    
    ...


    // 绑定事件
    clickme:function(e){
    // 点击以后会触发的一个log
    console.log("点击了跳转对象");
    // 获取传入的参数中的data-name参数, 用data-后面的名字进行获取
    var nid = e.currentTarget.dataset.nid;
    var name = e.currentTarget.dataset.name;
    console.log(nid);

    // 指定跳转对象
    wx.navigateTo({
      // 纯跳转
      // url: '/pages/redirect/redirect',
      // 跳转的同时，传入参数（nid）,利用字符串拼接生成参数格式（?attr=123&attr2=456）并传入
      // 跳转的目的页面的onLoad的function的options参数含有我们传入的参数 （redirect.js:15）
      url: '/pages/redirect/redirect?id='+nid+'&name='+name
    })
  }
})
```

### 1.2 页面跳转
```js
// 指定跳转对象
wx.navigateTo({
    // 纯跳转
    // url: '/pages/redirect/redirect',
    // 跳转的同时，传入参数（nid）,利用字符串拼接生成参数格式（?attr=123&attr2=456）并传入
    // 跳转的目的页面的onLoad的function的options参数含有我们传入的参数 （redirect.js:15）
    url: '/pages/redirect/redirect?id='+nid+'&name='+name
})
```
redirect.js onLoad function
```js
/**
 * 生命周期函数--监听页面加载
 * 在页面加载后，自动运行onload
 */
onLoad: function (options) {
    console.log(options);
}
```

