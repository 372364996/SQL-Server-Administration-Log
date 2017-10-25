## 使用WHERE子句

SQL过滤与应用过滤：建议在SQL中过滤数据，可以更快速；而且节省网络带宽。

WHERE子句的位置：WHERE子句位于FROM子句后面，ORDER BY子句前面。

```
SELECT prod_name, prod_price
FROM Products
WHERE prod_price = 3.49
```



