## 用到的技术
- 前端：jQuery+Bootstrap
- 后台：Node.js+Express
- 数据库：mongodb

## 系统简介
1.前端
- 主页（显示发布的博客）
- 博客标签以及不同标签下面的博客文章
- 关于我
- 留言

2.后台
- 发布博客
- 博客管理

## 遇到的问题
- Error: listen EADDRINUSE :::3000

解决：开启多个服务，占用一个端口，启动资源管理器，结束一个进程

- this._handle.update(data, encoding);TypeError: Data must be a string or a buffer

解决：将用户的注册信息存入数据库，我之前一直以为是md5加密部分错了，可是我在前端将$.post方法换成了$.ajax方法。通过对input标签
name属性，然后在后端用req.body.name的名称获取输入框的内容，然后用加密的算法，也能将密码进行加密，我初步猜测是form表单获取内容的错误。
我最后检查是因为在写路由的时候，路径前面少写了“/”.要特别注意路径的书写。

- 关于前端用jQuery处理Ajax请求，后端解析数据的方法,这次项目中我用到了这两种

1.使用req.body.inputName来处理数据，这个需要body-parser模块

2.使用formidable模块的parse方法
```
    var form = new formidable.IncomingForm();
    form.parse(req, function (err, fields, files) {
        //得到表单之后做的事情
        var username = fields.username;
        var password = fields.password;
        var md5PassWord = md5(md5(password).substr(4,7) + md5(password));
        db.insertOne("user1",{
            "username" : username,
            "password" : md5PassWord
        },function(err,result){
            if(err){
                res.send("-3");//服务器错误
                return;
            }
            req.session.login = "1";
            res.send("1");//注册成功，写入SESSION
        });
    });
```


