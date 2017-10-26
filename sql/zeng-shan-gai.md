## 插入（INSERT）

插入完整的行：

* 必须给每一列提供一个值，如果某列没有值，应该使用NULL值；
* 各列必须以它们在表定义中出现的顺序填充；

```
INSERT INTO Customers
VALUES('1000000006', 
       'Toy Land',
       '123 Any Street',
       'New York',
       'NY',
       '11111',
       'USA',
       NULL,
       NULL)；
```

特点：语法简单，但不安全，必须依赖列的顺序。

编写安全的语法如下：

```
INSERT INTO Customers([cust_id], 
                      [cust_name], 
                      [cust_address], 
                      [cust_city], 
                      [cust_state], 
                      [cust_zip], 
                      [cust_country], 
                      [cust_contact], 
                      [cust_email])
VALUES('1000000006', 
       'Toy Land',
       '123 Any Street',
       'New York',
       'NY',
       '11111',
       'USA',
       NULL,
       NULL);
```

推荐使用总是给出列名的INSERT语句。这样即使表列顺序发生变化，依然可以成功执行。

插入部分行：

可以省略自动设置默认值或允许为NULL的列。

```
INSERT INTO Customers([cust_id], 
                      [cust_name], 
                      [cust_address], 
                      [cust_city], 
                      [cust_state], 
                      [cust_zip], 
                      [cust_country])
VALUES('1000000006', 
       'Toy Land',
       '123 Any Street',
       'New York',
       'NY',
       '11111',
       'USA');
```

插入检索出的数据：

* 从新表NewCust中选择**所有行**插入到Customers表中，当然，SELECT语句可以包含WHERE子句用来过滤想要插入的数据；
* 不要求INSERT和SELECT语句的列名匹配，它是根据列的位置来填充的；
* 普通的INSERT语句只插入一行数据，INSERT SELECT语句是个例外，SELECT返回多少行就插入多少行；

```
INSERT INTO Customers([cust_id]
                    , [cust_name]
                    , [cust_address]
                    , [cust_city]
                    , [cust_state]
                    , [cust_zip]
                    , [cust_country]
                    , [cust_contact]
                    , [cust_email])
SELECT [cust_id]
     , [cust_name]
     , [cust_address]
     , [cust_city]
     , [cust_state]
     , [cust_zip]
     , [cust_country]
     , [cust_contact]
     , [cust_email]
FROM NewCust；
```

从一个表复制到另一个表：

* SELECT INTO语句用于将数据复制到一个新表，如果新表已存在则报错；
* 想要只复制某部分列，可以给出列名，而不使用通配符（\*）；
* 任何SELECT选项和子句都可以使用，包括WHERE和GROUP BY；
* 可以使用[联结（join）](/sql/lian-jie-ff08-join.md)从多个表插入数据；
* 不管从多少个表中检索数据，数据只能插入到一张表中。

```
SELECT *
INTO CustCopy
FROM Customers；
```

## 更新（UPDATE）

* 没有WHERE子句时，会更新整个表的所有行，**应该避免**这样做。

例如：更新客户1000000005的现有电子邮件：

```
UPDATE Customers
SET cust_email = 'kim@thetoystore.com'
WHERE cust_id = '1000000005'；
```

更新多个列时，只是用一个SET命令：

```
UPDATE Customers
SET cust_email = 'kim@thetoystore.com',
    cust_contact = 'Sam Roberts'
WHERE cust_id = '1000000005';
```

在UPDATE中使用子查询：

```
UPDATE Customers
SET cust_email = 'kim@thetoystore.com',
    cust_contact = (SELECT cust_contact 
                    FROM CustCopy 
                    WHERE cust_id = '1000000005')
WHERE cust_id = '1000000005';
```

要删除某个列的值，可将它设为NULL（NULL表示没有值）；

```
UPDATE Customers
SET cust_email = NULL
WHERE cust_id = '1000000005';
```

## 删除（DELETE）

* FROM关键字可选，但建议加上；
* DELECT删除行，如果要删除列，请使用UPDATE；
* DELECT只能删除行，甚至是删除所有行，但不能删除表本身；

```
DELETE FROM Customers
WHERE cust_id = '1000000006';
```

更快的删除表中的数据：

如果要删除表中的所有行，不要使用DELETE，要使用**TRUNCATE TABLE**语句，它完成相同的工作，而且速度更快。

```
TRUNCATE TABLE [dbo].[CustCopy]
```



