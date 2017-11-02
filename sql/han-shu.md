## 计算字段

计算字段是在运行时在SELECT语句中创建的。

使用加号（+）拼接字段：

拼接是将多个值连接在一起构成单个值。

```
SELECT vend_name + ' (' + vend_country + ')'
FROM Vendors
ORDER BY vend_name;

-- Bears R Us                                         (USA                                               )
```

数据库保存拼接成一个字段的两个列的列宽的文本值（空格），要去掉这些空格，可以使用RTRIM\(\)函数来完成。

```
SELECT RTRIM(vend_name) + ' (' + RTRIM(vend_country) + ')'
FROM Vendors
ORDER BY vend_name;

-- Bear Emporium (USA)
```

使用AS关键字为列赋予别名：

AS关键字可选，但最佳实践是加上AS关键字。

别名的用途：

* 使数据库列名包含不合法字符（例如空格）时重新命名它；
* 为拼接列指定列名称；
* 列名含混不清时扩充它。

```
SELECT RTRIM(vend_name) + ' (' + RTRIM(vend_country) + ')'
AS vend_title
FROM Vendors
ORDER BY vend_name;
```

算数运算符：

| 运算符 | 说明 | 运算符 | 说明 |
| :---: | :---: | :---: | :---: |
| + | 加 | - | 减 |
| \* | 乘 | / | 除 |
| % | 取余 |  |  |

算数计算：

```
SELECT 
    prod_id, 
    quantity, 
    item_price, 
    quantity * item_price AS expanded_price    --这是一个计算列
FROM OrderItems
WHERE order_num = 20008;
```

SELECT配合FROM表示从数据库中检索数据，单独使用时表示简单的访问和处理表达式。

例如：

```
SELECT 2 * 3;                --返回6
SELECT RTRIM('ABC    ');     --返回abc
SELECT GETDATE();            --返回当前时间
```

## 文本处理函数

| 函数 | 说明 |
| :--- | :--- |
| LEFT\(\) | \*返回字符串左边的字符 |
| LENGTH\(\) | 返回字符串的长度 |
| LOWER\(\) | 将字符串转换为小写 |
| LTRIM\(\) | 去掉字符串左边的空格 |
| RIGHT\(\) | \*返回字符串右边的字符 |
| RTRIM\(\) | 去掉字符串右边的空格 |
| SOUNDEX\(\) | \*返回字符串的SOUNDEX值（将任何文本串转换为描述其语音表示的字母数字模式的算法——即进行发音比较，匹配发音类似的字符） |
| UPPER\(\) | 将字符串转换为大写 |

UPPER：

```
SELECT 
    vend_name, 
    UPPER(vend_name) AS vender_name_upcase
FROM Vendors
ORDER BY vend_name;
```

SOUNDEX：匹配所有发音类似于Michael Green的联系人：

```
SELECT cust_name, cust_contact
FROM Customers
WHERE SOUNDEX(cust_contact) = SOUNDEX('Michael Green');    --OUTPUT：Kids Place | Michelle Green
```

## 日期和时间处理函数

| 函数 | 说明 |
| :--- | :--- |
| DATEPART\('返回的成分', '从中返回成分的日期'\) | 返回日期的某一部分 |

DATEPART：

```
SELECT order_num, order_date
FROM Orders
WHERE DATEPART(YYYY,order_date) = 2012;
```

## 数值处理函数

用于代数、三角或几何运算。

| 函数 | 说明 |
| :--- | :--- |
| ABS\(\) | 返回一个数的绝对值 |
| COS\(\) | 返回一个角度的余弦 |
| EXP\(\) | 返回一个数的指数值 |
| PI\(\) | 返回圆周率 |
| SIN\(\) | 返回一个角度的正弦 |
| SQRT\(\) | 返回一个数的平方根 |
| TAN\(\) | 返回一个角度的正切 |

## 聚集函数

| 函数 | 说明 |
| :--- | :--- |
| AVG\(\) | 返回某列的平均值 |
| COUNT\(\) | 返回某列的行数 |
| MAX\(\) | 返回某列的最大值 |
| MIN\(\) | 返回某列的最小值 |
| SUM\(\) | 返回某列的值之和 |

AVG：

* 该函数只能用于单个列；
* 忽略列值为NULL的行；

```
SELECT AVG(prod_price) AS avg_price
FROM Products;
--6.823333
```

COUNT：

* COUNT\(\*\)包含列值为NULL的行；
* COUNT\(column\)忽略列值为NULL的行；

```
SELECT COUNT(*) AS num_cust
FROM Customers;
```

MAX和MIN：

* 常用于找出最大的数值或日期；
* 也可用于返回文本列中排序在最后的值；
* 忽略列值为NULL的行；

```
SELECT MAX(prod_price) AS max_price
FROM Products;
```

```
SELECT MIN(prod_price) AS min_price
FROM Products;
```

SUM：

* 可用于多个列上的计算，例如SUM\(item\_price \* quantity\)先对一行的两个列求乘积，在累加所有列的和返回；
* 忽略列值为NULL的行；

计算订单号20005的商品数量：

```
SELECT SUM(quantity) AS items_ordered
FROM OrderItems
WHERE order_num = 20005;
```

合计订单号20005的总金额：

```
SELECT SUM(item_price * quantity) AS total_price
FROM OrderItems
WHERE order_num = 20005;
```

## 聚合不同值

在聚合函数的参数前面增加DISTINCT关键字，只聚合不同的数值。

* DISTINCT不能用于COUNT\(\*\)，DISTINCT只能用于列名前面，不能用于计算或表达式；
* DISTINCT用在MIN和MAX函数上是没有价值；
* 与DISTINCT关键字相对的是ALL关键字，默认为ALL关键字参数；

例如AVG：

```
SELECT AVG(DISTINCT prod_price)
FROM Products;
```

## 组合聚集函数

```
SELECT 
    COUNT(prod_id) AS num_items,
    MIN(prod_price) AS min_price,
    MAX(prod_price) AS max_price,
    AVG(prod_price) AS avg_price
FROM Products;
```



