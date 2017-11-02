## 子查询

子查询是嵌套在查询中的查询。在SELECT语句中，子查询总是从内向外处理。

子查询常用语WHERE子句的IN操作符中，以及用来填充计算列。

例如：列出订购商品RGAN01的顾客的信息（提示：顾客信息在Customers表中，顾客订单在Orders表中，订单详情在OrderItems表中）：

```
SELECT cust_name, cust_contact
FROM Customers
WHERE cust_id IN(SELECT cust_id
                 FROM Orders
                 WHERE order_num IN(SELECT order_num
                                    FROM OrderItems
                                    WHERE prod_id = 'RGAN01'
                                    )
                )
```

子查询对于嵌套的层次数量没有限制，但在实际使用时，嵌套层次越多性能越差。

作为子查询的SELECT语句**只能查询单个列**。

## 作为计算字段使用子查询

这个例子中使用了完全限定列名Orders.cust\_id和Customers.cust\_id，应用在WHERE子句中表示：比较Orders表中的cust\_id和当前正从Customers表中检索出的cust\_id。

```
SELECT
	cust_name,
	(SELECT COUNT(*) 
	 FROM Orders 
	 WHERE Orders.cust_id = Customers.cust_id) AS orders
FROM Customers
ORDER BY cust_name;
```



