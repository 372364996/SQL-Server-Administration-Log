## 事务

事务是一种机制，用来管理必须成批执行的SQL操作，保证数据库不包含不完整的操作结果。

事务（transaction）：一组SQL语句。

回退（rollback）：撤销执行SQL语句的过程。

提交（commit）：将未存储的SQL语句结果写入数据库。

保留点（savepoint）：事务处理中设置的临时占位符，可以对它发布回退。

可以回退的语句：

* INSERT、UPDATE、DELETE语句可以回退；
* SELECT语句不能回退（没有必要）；
* CREATE和DROP操作也不能回退，但事务中可以使用这些语句，只是操作不能撤销。

## 事务的语法

在事务处理块中，DELETE操作（包括UPDATE和INSERT）执行后并不会真正的操作数据库，需要进行明确的提交。在事务外面，这些操作会直接操作数据库表，这是隐式提交，是自动进行的。

```
-- 开始事务
BEGIN TRANSACTION
DELETE FROM Orders;
-- 回退
ROLLBACK
-- 放置保留点
SAVE TRANSACTION delete1;
-- 回退到指定的保留点
ROLLBACK TRANSACTION delete1;
-- 提交
COMMIT TRANSACTION
```

一个完整的例子：

```
-- 开始事务
BEGIN TRANSACTION
-- 插入一条顾客
INSERT INTO Customers(cust_id, 
					  cust_name)
			   VALUES('1000000010',
					  'Toys Emporium');
-- 放置保留点
SAVE TRANSACTION StartOrder;
-- 插入一条订单
INSERT INTO Orders(order_num, 
				   order_date,
				   cust_id)
			VALUES(20100,
				   '2001/12/01',
				   '1000000010');
-- 如果有错误，回退到保留点
IF @@ERROR <> 0 
	ROLLBACK TRANSACTION StartOrder;
-- 插入一条订单详情
INSERT INTO OrderItems(order_num,
					   order_item,
					   prod_id,
					   quantity,
					   item_price)
				VALUES(20100,
					   1,
					   'BR01',
					   100,
					   5.49);
-- 如果有错误，回退到保留点
IF @@ERROR <> 0
	ROLLBACK TRANSACTION StartOrder;
-- 插入一条订单详情
INSERT INTO OrderItems(order_num,
					   order_item,
					   prod_id,
					   quantity,
					   item_price)
				VALUES(20100,
					   2,
					   'BR03',
					   100,
					   10.99);
-- 如果有错误，回退到保留点
IF @@ERROR <> 0
	ROLLBACK TRANSACTION StartOrder;
-- 提交事务
COMMIT TRANSACTION
```



