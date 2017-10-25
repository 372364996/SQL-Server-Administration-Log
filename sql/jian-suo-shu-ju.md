# 使用SELECT语句检索数据

关键字（keyword）：

构成SQL语句的保留字，不能作为表或列的名字。

结束SQL语句时使用分号（;）；

SQL语句**不区分大小写**；

在处理SQL语句时，所有空格都被忽略，因此SQL语句可以写成长长的一行，也可以分写在多行。

多数开发者认为：

* 对SQL关键字使用大写，对表明和列名使用小写，更容易阅读和调试；
* 将SQL语句分成多行，更容易阅读和调试；

## 检索单个列

```
SELECT prod_name
FROM Products
```

## 检索多个列

必须在列名之间加上逗号，在最后一个列名后面不能加逗号，否则报错。

```
SELECT prod_name, prod_price, prod_desc
FROM Products
```



