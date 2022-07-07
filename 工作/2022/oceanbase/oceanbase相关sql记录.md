# visible和invisible

oms迁移后会新生成4个oms列，需要删除。

```
alter table 表名 modify 字段 visible||invisible;
```



# 索引

oms迁移后会对新生成的4个oms列创建一个唯一索引。

海东青可以在报错语句下面，点击sql查看完整带参数的sql语句。

![image-20220705093102941](../../../img/image-20220705093102941.png)