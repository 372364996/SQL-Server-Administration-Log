## 触发器

触发器是特殊的存储过程（只与单个表关联），它在特定的数据库活动发生时自动执行。触发器可以与指定表上的INSERT、UPDATE、DELETE操作相关联。

触发器的常见用途：

* 基于某个表的变动在其他表上执行活动，例如在更新一张表时在日志表中记录一条日志；
* 进行额外的验证并根据需要回退数据；
* 计算计算列的值或更新时间戳；

创建触发器：

```
CREATE TRIGGER customer_state
ON Customers
FOR INSERT, UPDATE
AS
UPDATE Customers
SET cust_state = UPPER(cust_state)
WHERE Customers.cust_id = inserted.[cust_id];
```

注意：**约束的处理速度比触发器更快**。

