## 使用WHERE子句

SQL过滤与应用过滤：建议在SQL中过滤数据，可以更快速；而且节省网络带宽。

WHERE子句的位置：WHERE子句位于FROM子句后面，ORDER BY子句前面。

```
SELECT prod_name, prod_price
FROM Products
WHERE prod_price = 3.49
```

## WHERE子句操作符

| 操作符 | 说明 | 操作符 | 说明 |
| :---: | :--- | :---: | :--- |
| = | 等于 | &gt; | 大于 |
| &lt;&gt; | 不等于 | &gt;= | 大于等于 |
| != | 不等于 | !&gt; | 不大于 |
| &lt; | 小于 | BETWEEN......AND...... | 在指定的两个值之间 |
| &lt;= | 小于等于 | IS NULL | 为NULL的值 |
| !&lt; | 不小于 |  |  |

## 不匹配检查

无法返回vend\_id 为NULL的列，因为未知（unknown）具有特殊的含义，数据库不知道它是否匹配。

```
SELECT vend_id, prod_name
FROM Products
WHERE vend_id <> 'DLL01'
```

## 范围检查

BETWEEN关键字，必须指定两个值——所需范围的低端值和高端值，这两个值必须用AND分隔。

```
SELECT prod_name, prod_price
FROM Products
WHERE prod_price BETWEEN 5 AND 10
```

## 空值检查

在一个列不包含值时，称其包含空值NULL。在创建表时，可以指定列是否能不包含值。

```
SELECT cust_name
FROM Customers
WHERE cust_email IS NULL
```



