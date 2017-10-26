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

## 内联结（INNER JOIN）：

基于两个表之间相等的测试，这种联结称为内联结，也成为等值联结（EQUIjoin）。

```
SELECT vend_name, prod_name, prod_price
FROM Vendors
INNER JOIN Products
ON Vendors.vend_id = Products.vend_id
```

这个语句与上面使用WHERE的语句效果相同，**ANSI SQL规范首选INNER JOIN语法**。

性能考虑：

尽量减少联结的表的数量，联结的表数量越多，性能下降越厉害。

表别名：

表别名只在查询执行中使用，与列别名不同，表别名不返回到客户端。

```
SELECT C.cust_name, C.cust_contact
FROM Customers AS C
INNER JOIN Orders AS O
ON C.cust_id = O.cust_id
INNER JOIN OrderItems AS OI
ON O.order_num = OI.order_num
WHERE OI.prod_id = 'RGAN01'
```

## 自联结

例如：列出Jim Jones这个人工作的公司的所有员工（提示：cust\_name保存的是公司名，cust\_contact保存的是员工名）：

```
SELECT C1.cust_id, C1.cust_name, C1.cust_contact
--,C2.cust_id, C2.cust_name, C2.cust_contact
FROM Customers AS C1
INNER JOIN Customers AS C2
ON C1.cust_name = C2.cust_name
WHERE C2.cust_contact = 'Jim Jones'
```

也可使用如下语句（更容易理解）：

```
SELECT cust_id, cust_name, cust_contact
FROM Customers
WHERE cust_name IN(SELECT cust_name
                   FROM Customers
                   WHERE cust_contact = 'Jim Jones'
                   )
```

## 自然联结

即在联结查询时，排除重复出现的列，保证每个列只出现一次。

## 外联结（OUTER JOIN）

外联结包含了那些在相关表中没有关联的行。

使用OUTER JOIN语法时，必须指定RIGHT或LEFT关键字指定**包括其所有行的表**（RIGHT指出的是OUTER JOIN右边的表，而LEFT指出的是OUTER JOIN左边的表）。因此有两种形式的外联结：左外联结和右外联结，它们唯一的区别是所关联的表的顺序。

左外联结示例：

```
SELECT C.cust_id, O.order_num
FROM Customers AS C
LEFT OUTER JOIN Orders AS O
ON C.cust_id = O.cust_id

-- cust_id       order_num
---------------------------
-- 1000000001    20005
-- 1000000001    20009
-- 1000000002    NULL
-- 1000000003    20006
-- 1000000004    20007
-- 1000000005    20008
```

右外联结示例：

```
SELECT C.cust_id, o.order_num
FROM Customers AS C
RIGHT OUTER JOIN Orders AS O
ON C.cust_id = O.cust_id

-- cust_id       order_num
---------------------------
-- 1000000001    20005
-- 1000000003    20006
-- 1000000004    20007
-- 1000000005    20008
-- 1000000001    20009
```

还有一种连接：全外联结（full outer join），它检索两个表中所有行并关联那些可以关联的行。全外联结包含两个表的不关联的行。

```
SELECT C.cust_id, o.order_num
FROM Customers AS C
FULL OUTER JOIN Orders AS O
ON C.cust_id = O.cust_id

-- cust_id	order_num
---------------------------
-- 1000000001	20005
-- 1000000001	20009
-- 1000000002	NULL
-- 1000000003	20006
-- 1000000004	20007
-- 1000000005	20008
```



