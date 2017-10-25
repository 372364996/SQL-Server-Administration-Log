# 使用SELECT语句检索数据

关键字（keyword）：

构成SQL语句的保留字，不能作为表或列的名字。

结束SQL语句时使用分号（;）；

SQL语句**不区分大小写**；

在处理SQL语句时，所有空格都被忽略，因此SQL语句可以写成长长的一行，也可以分写在多行。

多数开发者认为：

* 对SQL关键字使用大写，对表明和列名使用小写，更容易阅读和调试；
* 将SQL语句分成多行，更容易阅读和调试；
* 最好不使用通配符（\*），检索不需要的列会降低检索和应用程序的性能；

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

## 检索所有列

```
SELECT *
FROM Products
```

## 检索不同的值

检索某一列时，不希望有重复的值时，可以使用**DISTINCT**关键字，必须放在列名的前面，它指数据库只返回不同的值。DISTINCT关键字作用于所有的列，不仅仅是跟在后面的那一列。

```
SELECT DISTINCT vend_id
FROM Products
```

## 限制结果

**TOP**关键字限制返回从第0行开始一定数量的行。

```
SELECT TOP 5 prod_name
FROM Products
```

## 使用注释

```
-- 这是单行注释

/*
   这是多行注释
*/
```



