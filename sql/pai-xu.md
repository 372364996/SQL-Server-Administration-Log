# 使用SELECT语句的ORDER BY子句排序检索出来的数据

关系数据库设计理论认为，如果不明确规定排序顺序，则不应该检索出来的数据具有任何意义。

## 排序

**ORDER BY**子句的位置：

应保证它是SELECT语句的最后一条子句，否则将出现错误。

ORDER BY子句可以使用检索出来的列排序，也可以使用非检索出来的列排序。

```
SELECT prod_name
FROM Products
ORDER BY prod_name
```

## 按多个列排序

在按多个列排序时，排序的顺序是：首先按照ORDER BY子句后面第一个列名的值进行排序，该值相同时，相同列按照第二个列名排序；如果第一个列名的值都是唯一的，则不会按照第二个列名的值排序。

```
SELECT prod_id, prod_name, prod_price
FROM Products
ORDER BY prod_price, prod_name
```

## 指定排序方向

DESC关键字（DESCENDING的缩写）：指定降序排序（Z-A），数据库默认排序为升序排序（A-Z），即ASC关键字（ASCENDING的缩写）。

DESC关键字只应用到直接位于前面的列名，如果想在多个列上进行降序排序，必须对每一列指定DESC关键字

```
SELECT prod_id, prod_price, prod_name
FROM Products
ORDER BY prod_price DESC, prod_name
```



