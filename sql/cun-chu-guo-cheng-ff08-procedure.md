## 存储过程

优点：

* 存储过程通常以编译过的形式存储，提高性能；
* 存储过程可以编写功能更强更灵活的代码；
* 处理封装在一个单元中，简化操作；

## 创建

* DECLARE关键字用于声明存储过程内部的局部变量；
* SQL Server中所有局部变量名都以@开头；
* RETURN关键字用于返回结果；

```
CREATE PROCEDURE MailingListCount
AS
DECLARE @cnt INTEGER        --声明局部变量
SELECT @cnt = COUNT(*)
FROM Customers
WHERE NOT cust_email IS NULL;
RETURN @cnt;
```

执行：

```
DECLARE @RetureValue INT;                    --声明局部变量
EXECUTE @RetureValue = MailingListCount;
SELECT @RetureValue;
```



