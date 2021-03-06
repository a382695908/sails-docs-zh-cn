# 布局
当构建一个app带有许多不同的页面的时候，将几个HTML文件共享的标记独立出一个布局文件是很有用的。这[直接减少你的工程中的代码量](http://en.wikipedia.org/wiki/Don't_repeat_yourself)并帮助你避免一段时间之后在多个文件中做同样的改动。

在Sails和Express中，布局是模板引擎自己实现的。比如，Jade有自己的布局系统，使用的是自己的语法。

为了方便，**当使用默认引擎EJS的时候**Sails会绑定一些布局的特殊支持。如果你想使用不同的模板引擎，请查看[模板引擎文档](http://sailsjs.org/documentation/concepts/Views/ViewEngines.html)以找到对应的语法。

### 创建布局文件
在你的`views/`文件夹下Sails的布局是特殊的`.ejs`文件。布局文件内容经常包含一个头部(比如`!DOCTYPE html<html><head>....</head><body>`)和结尾(`</body></html>`)。然后使用`<%- body %>`包含原始的视图文件。布局文件如果没有一个视图是绝不会被使用的。

在[`config/views.js`](http://sailsjs.org/documentation/anatomy/myApp/config/views.js.html)文件中可以配置或者禁用布局支持，并且可以通过设置一个特殊的local叫做`layout`来为一个特别的路由或动作重写布局文件。默认Sails会编译所有位于`views/layout.ejs`的使用布局的视图。

为了指定一个视图使用的布局，参考下面的例子。更多信息在路由一节中。

下面的路由使用将会使用视图文件`/views/users/privacy.ejs`和布局文件`./views/users.ejs`。

```javascript
'get /privacy': {
    view: 'users/privacy',
    locals: {
      layout: 'users'
    }
  },
```

下面的控制器动作将会使用视图文件`./views/users/privacy.ejs`和布局文件`./views/users.ejs`：

```javascript
privacy: function (req, res) {
  res.view('users/privacy', {layout: 'users'})
}
```

### 注意：

> **为什么布局文件只是对EJS有用？**

> 在Express3，是不赞成内建支持的布局或者局部模板，开发者被希望依赖他们自己的模板引擎来实现这个特性。(参考https://github.com/balderdashy/sails/issues/494)

> 因为采取Express3，Sails为了方便选择支持传统的layouts特性，向后兼容Express 2.x和Sails 0.8.x app，尤其，那些来自其他MVC框架的新的社区成员。因此，布局只有使用默认的模板引擎EJS测试过。

> 如果布局不是你想要的，或者如果你正在使用一个服务器端的模板引擎而不是EJS(比如Jade、handlebars, haml, dust)，那么你应该在sails.config.views中设置layout:false，然后根据你的模板引擎自定义布局/局部模板支持。




<docmeta name="displayName" value="Layouts">
