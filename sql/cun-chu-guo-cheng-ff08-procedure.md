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
EXECUTE @RetureValue = MailingListCount;     --给局部变量赋值
SELECT @RetureValue;                         --检索
```

使用存储过程插入新订单的例子：

```
-- 传入参数@cust_id
CREATE PROCEDURE NewOrder @cust_id CHAR(10)
AS
-- 创建局部变量
DECLARE @order_num INTEGER
-- 为局部变量赋值
SELECT @order_num = MAX(order_num)
FROM Orders
SELECT @order_num = @order_num + 1
-- 插入数据
INSERT INTO Orders(order_num, 
				   order_date, 
				   cust_id)
VALUES(@order_num,
	   GETDATE(),
	   @cust_id)
-- 返回结果
RETURN @order_num;
```

与上面不同的版本：

```
-- 输入参数@cust_id
CREATE PROCEDURE NewOrder @cust_id CHAR(10)
AS
-- 插入数据（id使用自增列，日期使用默认值GETDATE()函数）
INSERT INTO Orders(cust_id)
VALUES(@cust_id)
-- 全局变量@@IDENTITY用于得到自动生成的ID
SELECT order_num = @@IDENTITY;
```



