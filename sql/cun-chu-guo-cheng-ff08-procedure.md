## 存储过程

优点：

* 存储过程通常以编译过的形式存储，提高性能；
* 存储过程可以编写功能更强更灵活的代码；
* 处理封装在一个单元中，简化操作；

## 创建

```
CREATE PROCEDURE MailingListCount
AS
DECLARE @cnt INTEGER		--声明局部变量
SELECT @cnt = COUNT(*)
FROM Customers
WHERE NOT cust_email IS NULL;
RETURN @cnt;
```

## 执行



