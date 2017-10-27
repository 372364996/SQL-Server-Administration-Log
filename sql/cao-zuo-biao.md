## 创建表（CREATE TABLE）

* 如果列不指定NOT NULL，则默认为NULL；
* 关键字PRIMARY KEY用来标识主键，主键用来唯一标识列，只有NOT NULL的列才可指定为主键；
* 指定默认值使用DEFAULT关键字后面跟上要指定的值（例如：指定日期时使用DEFAULT GETDATE\(\)），建议优先使用DEFAULT而不是NULL；

```
CREATE TABLE Products2
(
    prod_id        CHAR(10)         NOT NULL PRIMARY KEY,
    vend_id        CHAR(10)         NOT NULL,
    prod_name      CHAR(254)        NOT NULL,
    prod_price     DECIMAL(8,2)     NOT NULL    DEFAULT 0.1,
    prod_desc      VARCHAR(1000)    NULL
);
```

## 更新表（ALTER TABLE）

使用ATLER TABLE之前要十分小心，应该做好数据的完整备份工作。

增加列：

```
ALTER TABLE [dbo].[Vendors]
ADD vend_phone    CHAR(20)    NULL;
```

删除列：

1. 使用新的列布局创建一个新表；
2. 使用INSERT SELECT语句将旧表数据复制到新表；
3. 检验包含所需数据的新表；
4. 重命名旧表；
5. 用旧表原来的名字重命名新表；
6. 根据需要，重新创建触发器、存储过程、索引和外键。

```
ALTER TABLE [dbo].[Vendors]
DROP COLUMN vend_phone;
```

## 删除表（DROP TABLE）

执行之后将永久删除表，使用之前应做好备份工作。

```
DROP TABLE CustCopy;
```

## 重命名表（sp\_rename）

```
sp_rename @objname = CustCopy, @newname = CustCopy2;
```



