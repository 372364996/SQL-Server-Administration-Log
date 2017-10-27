## 约束

定义：管理如何插入或处理数据库数据的规则；

## 主键

用来保证一列（或一组列）中的值是唯一的，而且永不改动。

第一种定义主键方法：

```
CREATE TABLE Products2
(
    prod_id        CHAR(10)         NOT NULL PRIMARY KEY,
    ...
);
```

第二种定义主键方法：

* PK\_PrimaryKeyName：指定这个主键约束的名字；

```
ALTER TABLE Vendors
ADD CONSTRAINT PK_PrimaryKeyName PRIMARY KEY (vend_id);
```

## 外键

用来保证**引用完整性**的及其重要的部分，其值必须在另一个表的主键中。外键有助于防止意外删除。如果启用**级联删除**功能，会自动删除关联的行。

第一种定义外键方法：

```
CREATE TABLE Products3
(
	prod_id CHAR(10) NOT NULL PRIMARY KEY,
	vend_id CHAR(10) NOT NULL REFERENCES Venders(vend_id),
	...
);
```

第二种定义外键方法：

* FK\_ForeignKeyName：指定这个外键约束的名字。

```
ALTER TABLE Products3
ADD CONSTRAINT FK_ForeignKeyName FOREIGN KEY (vend_id) REFERENCES Vendors(vend_id);
```

## 唯一约束

用来保证一列中的数据是唯一的，它与主键的区别如下：

* 表可以包含多个唯一约束，但每个表只能有一个主键；
* 唯一约束列可包含NULL值；
* 唯一约束列可修改或更新；
* 唯一约束列的值和重复使用（在执行删除操作后）；
* 唯一约束不能用来定义外键。

例如：员工表中，每个雇员有唯一的社会安全号，因为它太长，不想用来做主键，因此指定单独的雇员ID作为主键：

```
CREATE TABLE Employees
(
	ID INTEGER NOT NULL PRIMARY KEY,
	employ_id INTEGER NOT NULL UNIQUE,
	...
)
```



