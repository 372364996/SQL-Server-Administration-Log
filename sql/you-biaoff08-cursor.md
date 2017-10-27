## 游标

游标是一个存储在服务器上的数据库查询，它不是一条SELECT语句，而是被该语句检索出来的结果集。

使用游标：

* 在使用游标前，必须声明它。这个过程实际上没有检索数据，只是定义使用的SELECT语句和游标选项。
* 一旦声明，就必须打开游标以供使用，这个过程执行检索数据；
* 根据需要取出各行；
* 在结束游标使用时，必须关闭游标，释放游标。

## 创建游标

```
DECLARE CustCursor CURSOR
FOR
SELECT *
FROM Customers
WHERE cust_email IS NULL;
```



