# Flask实战小技巧（1）—— Flask-SQLalchemy中对于日期的筛选过滤

[![img](https://upload.jianshu.io/users/upload_avatars/6274961/5fa742e3-fe7b-460b-817e-814e9c765ab9?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/f15e05d2a0da)

[曲谐_](https://www.jianshu.com/u/f15e05d2a0da)关注

2019.08.08 13:14:34字数 349阅读 680

### 业务背景：

- 某些数据需要筛选后显示，如果是普通的筛选一般都是字符串或数字的形式，然而日期的形式很少用。当前业务需求对某一天的业务日志进行筛选。

### 思考：

- 在SQL中，筛选条件可以用where xx="2019-08-07"的写法，但在sqlalchemy中，对datetime数据类型的修改往往不能这么写。

### 解决方案：

采用sqlalchemy的extract函数和and函数。前者可比较年月日信息，后者可表示sql中的and。
实例：
接口采用POST方法，接口信息：



```json
{
    "date": "2019-08-07",
    "monitor_id": 1
}
```

- monitor_id为业务字段，可忽略，**重点来看date字段**。
- 需要比较的数据：**MonitorCameraList模型类中的updated_at字段，datetime类型，见下。**
- 接口传入的date字段是一个字符串，需要先转化成时间元组，可使用datetime的strptime方法。然后datetime中的year，month，day属性可以获取到年月日信息。这一步是很重要的，**因为接口传过来的都是变量，你不知道具体是哪一天的信息，因此一定要学会这种对变量做转化的方法**。



```swift
    query = MonitorCameraList.query.filter(
        MonitorCameraList.move_status == 1,
        MonitorCameraList.monitor_id == body["monitor_id"]
    )

    # 筛选条件
    if "date" in body:
        date_tuple = datetime.strptime(body["date"], "%Y-%m-%d")
        query = query.filter(and_(
                extract("year", MonitorCameraList.updated_at) == date_tuple.year,
                extract("month", MonitorCameraList.updated_at) == date_tuple.month,
                extract("day", MonitorCameraList.updated_at) == date_tuple.day
            )
        )
    sth_list = query.all()
```

------

使用extract过滤，sth_list字段就可以获得筛选后的结果了。



0人点赞



[Flask](https://www.jianshu.com/nb/39248230)