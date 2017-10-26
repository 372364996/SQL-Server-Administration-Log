## 关系表

关系表的设计就是要把信息分解成多个表，每个表存储一类信息，各表通过某些共同的值相互关联。

## 联结

联结是一种机制，用来在一条SELECT语句中关联表。

```
SELECT vend_name, prod_name, prod_price
FROM Vendors, Products
WHERE Vendors.vend_id = Products.vend_id
```

WHERE子句的重要性：在联结两个表时，实际要做的是将第一个表中的第一行与第二个表的所有行匹配，WHERE作为过滤条件，只包含哪些匹配给定条件的行。

笛卡尔积：

由没有联结条件的表返回的结果称为笛卡尔积，检索出的行的数目将是第一个表的行数乘以第二个表的行数。

叉联结（cross join）：

返回笛卡尔积的联结，称为叉联结。

内联结（inner join）：

基于两个表之间相等的测试，这种联结称为内联结，也成为等值联结（EQUIjoin）。

```
SELECT vend_name, prod_name, prod_price
FROM Vendors
INNER JOIN Products
ON Vendors.vend_id = Products.vend_id
```

这个语句与上面使用WHERE的语句效果相同，**ANSI SQL规范首选INNER JOIN语法**。



