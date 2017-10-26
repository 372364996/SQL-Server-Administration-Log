## 组合查询

UNION指示执行两个或多个SELECT语句，并把输出组合成一个查询结果集。

需要使用组合查询的情况：

* 在一个查询中从不同的表返回数据；
* 对一个表执行多个查询，按一个查询返回数据；

例如：列出在IL、IN、MI等几个州的所有顾客列表，以及所有在Fun4All工作的顾客：

```
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN('IL', 'IN', 'MI')
OR cust_name = 'Fun4All'

-- cust_name        cust_contact            cust_email
--------------------------------------------------------------
-- Village Toys     John Smith              sales@villagetoys.com
-- Fun4All          Jim Jones               jjones@fun4all.com
-- Fun4All          Denise L. Stephens      dstephens@fun4all.com
-- The Toy Store    Kim Howard              NULL
```

还可使用组合方式查询：

```
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN('IL', 'IN', 'MI')
UNION
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_name = 'Fun4All'

-- cust_name	cust_contact	cust_email
------------------------------------------------------------------
-- Fun4All		Denise L. Stephens		dstephens@fun4all.com
-- Fun4All		Jim Jones		jjones@fun4all.com
-- The Toy Store		Kim Howard		NULL
-- Village Toys		John Smith		sales@villagetoys.com
```



