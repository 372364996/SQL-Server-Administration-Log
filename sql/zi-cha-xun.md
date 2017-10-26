## 子查询

子查询是嵌套在查询中的查询。在SELECT语句中，子查询总是从内向外处理。

例如：列出订购商品

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



