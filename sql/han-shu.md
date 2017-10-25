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

SQL算数运算符：

| 运算符 | 说明 | 运算符 | 说明 |
| :---: | :---: | :---: | :---: |
| + | 加 | - | 减 |
| \* | 乘 | / | 除 |

算数计算：

```
SELECT 
	prod_id, 
	quantity, 
	item_price, 
	quantity * item_price AS expanded_price	--这是一个计算列
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



