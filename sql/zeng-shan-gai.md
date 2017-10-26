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



