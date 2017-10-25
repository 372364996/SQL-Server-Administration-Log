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
| &lt; | 小于 | BETWEEN | 在指定的两个值之间 |
| &lt;= | 小于等于 | IS NULL | 为NULL的值 |
| !&lt; | 不小于 |  |  |



