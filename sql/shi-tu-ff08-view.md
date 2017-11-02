## 视图

视图是虚拟的表，与包含数据的表不同，视图只是在需要的时候动态检索数据。

视图的常见应用：

* 重用SQL语句；
* 简化复杂的SQL操作；
* 使用表的一部分而不是整个表；
* 保护数据（可以授权用户访问表的特定部分，而不是整个表）；
* 更改数据格式和表示（视图可返回与底层表的表示和格式不同的数据）；

视图使用的规则和限制：

* 视图名必须唯一；
* 视图可以嵌套，即可以从其他视图的检索数据的查询来构造视图（嵌套视图可能会严重降低查询的性能）；
* 视图不能索引，也不能有关联的触发器或默认值；

## 创建视图

例如：列出已订购产品的所有顾客：

```
CREATE VIEW VW_ProductCustomers
AS
SELECT cust_name, cust_contact, prod_id
FROM Customers AS C
INNER JOIN Orders AS O
ON C.cust_id = O.cust_id
INNER JOIN OrderItems AS OI
ON O.order_num = OI.order_num;
```

查询视图：

```
SELECT cust_name, cust_contact
FROM VW_ProductCustomers
WHERE prod_id = 'RGAN01';
```

## 删除视图

```
DROP VIEW VW_ProductCustomers;
```

## 重命名视图

必须先删除视图在重新创建。

