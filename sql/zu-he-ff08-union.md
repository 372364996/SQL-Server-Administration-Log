## 组合查询

UNION指示执行两个或多个SELECT语句，并把输出组合成一个查询结果集，并自动排除了重复的行。

需要使用组合查询的情况：

* 在一个查询中从不同的表返回数据；
* 对一个表执行多个查询，按一个查询返回数据；

使用UNION应该遵循：

1. 必须有两条或两条以上的SELECT语句组成，语句之间用UNION关键字分隔；
2. 每个SELECT查询必须包含相同的列、表达式、聚集函数（但不需要以相同的列顺序）；
3. 列数据类型必须兼容（含隐式转换）；

例如：列出在IL、IN、MI等几个州的所有顾客列表，以及所有在Fun4All工作的顾客：

```
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN('IL', 'IN', 'MI')
OR cust_name = 'Fun4All';

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
WHERE cust_name = 'Fun4All';

-- cust_name         cust_contact            cust_email
------------------------------------------------------------------
-- Fun4All           Denise L. Stephens      dstephens@fun4all.com
-- Fun4All           Jim Jones               jjones@fun4all.com
-- The Toy Store     Kim Howard              NULL
-- Village Toys      John Smith              sales@villagetoys.com
```

## 包含或取消重复的行

UNION默认排除了重复的行，使用UNION ALL将返回所有匹配的行。

```
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN('IL', 'IN', 'MI')
UNION ALL
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_name = 'Fun4All';

-- cust_name         cust_contact            cust_email
------------------------------------------------------------------
-- Fun4All           Denise L. Stephens      dstephens@fun4all.com
-- Fun4All           Jim Jones               jjones@fun4all.com
-- The Toy Store     Kim Howard              NULL
-- Fun4All           Jim Jones               jjones@fun4all.com
-- Village Toys      John Smith              sales@villagetoys.com
```



