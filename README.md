## �õ��ļ���
- ǰ�ˣ�jQuery+Bootstrap
- ��̨��Node.js+Express
- ���ݿ⣺mongodb

## ϵͳ���
1.ǰ��
- ��ҳ����ʾ�����Ĳ��ͣ�
- ���ͱ�ǩ�Լ���ͬ��ǩ����Ĳ�������
- ������
- ����
2.��̨
- ��������
- ���͹���

## ����������
- Error: listen EADDRINUSE :::3000

����������������ռ��һ���˿ڣ�������Դ������������һ������

- this._handle.update(data, encoding);TypeError: Data must be a string or a buffer

��������û���ע����Ϣ�������ݿ⣬��֮ǰһֱ��Ϊ��md5���ܲ��ִ��ˣ���������ǰ�˽�$.post����������$.ajax������ͨ����input��ǩ
name���ԣ�Ȼ���ں����req.body.name�����ƻ�ȡ���������ݣ�Ȼ���ü��ܵ��㷨��Ҳ�ܽ�������м��ܣ��ҳ����²���form����ȡ���ݵĴ���
�����������Ϊ��д·�ɵ�ʱ��·��ǰ����д�ˡ�/��.Ҫ�ر�ע��·������д��
- ����ǰ����jQuery����Ajax���󣬺�˽������ݵķ���,�����Ŀ�����õ���������
1.ʹ��req.body.inputName���������ݣ������Ҫbody-parserģ��
2.ʹ��formidableģ���parse����
```
    var form = new formidable.IncomingForm();
    form.parse(req, function (err, fields, files) {
        //�õ���֮����������
        var username = fields.username;
        var password = fields.password;
        var md5PassWord = md5(md5(password).substr(4,7) + md5(password));
        db.insertOne("user1",{
            "username" : username,
            "password" : md5PassWord
        },function(err,result){
            if(err){
                res.send("-3");//����������
                return;
            }
            req.session.login = "1";
            res.send("1");//ע��ɹ���д��SESSION
        });
    });
```


