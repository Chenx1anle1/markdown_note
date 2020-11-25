# Flask-Sqlalchemy的relationship, backref

[![img](https://upload.jianshu.io/users/upload_avatars/11589058/efc291c4-eed0-49e2-b329-f9bf0846ae7f?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/475b5e07c9ed)

[旭日丶丶](https://www.jianshu.com/u/475b5e07c9ed)关注

0.0662019.09.27 16:42:13字数 292阅读 835

先放上代码:



```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:////tmp/test.db'
db = SQLAlchemy(app)


class User(db.Model):
    __tablename__ = "User"
    id = db.Column(db.Integer, primary_key=True)
    UserName = db.Column(db.String(80), nullable=False)

    addresses = db.relationship('Address', backref='User', lazy='select')

    def __repr__(self):
        return '<User %r>' % self.UserName

class Address(db.Model):
    __tablename__ = "Address"
    id = db.Column(db.Integer, primary_key=True)
    Address = db.Column(db.String(80), unique=True, nullable=False)

    User_Name = db.Column(db.String(80), db.ForeignKey('User.UserName'))


    def __repr__(self):
        return '<Address %r>' % self.Address


if __name__ == "__main__":
    db.drop_all()
    db.create_all()
    user = User(UserName='tom')
    address = Address(Address='fff', User_Name=user.UserName)
    db.session.add(user)
    db.session.add(address)
    db.session.commit()
    import pdb
    pdb.set_trace()

    print('11')
```

简单的`一对多`关系, 一个用户可以拥有多个地址

##### 1. 先在Address表里加入外键:



```python
User_Name = db.Column(db.String(80), db.ForeignKey('User.UserName'))
```

##### 2. 再在user表里加上关系



```python
addresses = db.relationship('Address', backref='User', lazy='select')
```

- `backref`表示在address表的对象访问User的时候的加载方式, 比如`add1.User`
- `lazy`表示User对象访问addresses的加载方式, 比如`user1.addresses`
    1) 默认为`select` 延迟加载, 返回的是一个`InstrumentedList`, 可以直接作为一个对象使用:



```python
print(user1.addresses) #output: [<Address 'fff'>]
```

​    2) 通常情况下我们会用`dynamic`方式, 因为这时会返回一个`Query`对象`sqlalchemy.orm.dynamic.AppenderBaseQuery`, 这样我们就可以在user1.addresses上使用filter了, 比如:



```python
user1.addresses.filter(Address.Address=='Beijing')
```

`lazy`的其他用法, 在[官方文档](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.sqlalchemy.org%2Fen%2F13%2Form%2Frelationship_api.html%23sqlalchemy.orm.relationship)
)已经说得很清楚了, 性能方面的优化用法视情况使用, 一般情况下我们只需要考虑`dynamic`方式就可以

##### 3. 多对多关系

具体范例参考[官网范例](https://links.jianshu.com/go?to=https%3A%2F%2Fdocs.sqlalchemy.org%2Fen%2F13%2Form%2Ftutorial.html%23orm-tutorial-many-to-many) 这里只提2点:

- `relationship`新增了一个参数`secondary`, 赋值为一个新的关系表
- `backref`可以赋值为



```python
addresses = db.relationship('Address', secondary=User_Address, backref=backref('Users', lazy='dynamic'), lazy='dynamic')
```

这样当你调用`add1.Users`, 就也可以用`filter`了



```python
add1.Users.filter(User.UserName=='tom')
```

这样就可以双向`dynamic`引用`Query`对象啦