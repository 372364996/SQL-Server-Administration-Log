## 游标

游标是一个存储在服务器上的数据库查询，它不是一条SELECT语句，而是被该语句检索出来的结果集。

使用游标：

* 在使用游标前，必须声明它。这个过程实际上没有检索数据，只是定义使用的SELECT语句和游标选项。
* 一旦声明，就必须打开游标以供使用，这个过程执行检索数据；
* 根据需要取出各行；
* 在结束游标使用时，必须关闭游标，释放游标。

## 创建游标（DECLARE CURSOR）

所有没有邮箱的顾客：

```
DECLARE CustCursor CURSOR
FOR
SELECT *
FROM Customers
WHERE cust_email IS NULL;
```

## 使用游标

打开游标（OPEN）：

```
OPEN CustCursor;
```

使用游标（FETCH）：

```
FETCH NEXT FROM CustCursor
```

关闭游标（CLOSE）：

```
CLOSE CustCursor;
```

释放游标（DE）：

```
DEALLOCATE CustCursor;
```

完整示例：

* @@FETCH\_STATUS：返回针对连接当前打开的任何游标发出的最后一条游标 FETCH 语句的状态。

```
DECLARE @cust_id         CHAR(10),
        @cust_name       CHAR(50),
        @cust_address    CHAR(50),
        @cust_city       CHAR(50),
        @cust_state      CHAR(5),
        @cust_zip        CHAR(10),
        @cust_country    CHAR(50),
        @cust_contact    CHAR(50),
        @cust_email      CHAR(255)
-- 打开游标
OPEN CustCursor;
-- 使用
FETCH NEXT FROM CustCursor
    INTO @cust_id,
         @cust_name,
         @cust_address,
         @cust_city,
         @cust_state,
         @cust_zip,
         @cust_country,
         @cust_contact,
         @cust_email
    WHILE @@FETCH_STATUS = 0
BEGIN
FETCH NEXT FROM CustCursor
    INTO @cust_id,
         @cust_name,
         @cust_address,
         @cust_city,
         @cust_state,
         @cust_zip,
         @cust_country,
         @cust_contact,
         @cust_email
...
END
-- 关闭游标
CLOSE CustCursor;
-- 删除游标引用，释放游标
DEALLOCATE CustCursor;
```



