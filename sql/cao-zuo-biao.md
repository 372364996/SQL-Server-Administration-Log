## 创建表（CREATE TABLE）

* 如果列不指定NOT NULL，则默认为NULL；
* 主键用来唯一标示列，只有NOT NULL的列才可指定为主键；
* 指定默认值使用DEFAULT关键字后面跟上要指定的值（例如：指定日期时使用DEFAULT GETDATE\(\)），建议优先使用DEFAULT而不是NULL；

```
CREATE TABLE Products2
(
	prod_id		CHAR(10)		NOT NULL,
	vend_id		CHAR(10)		NOT NULL,
	prod_name	CHAR(254)		NOT NULL,
	prod_price	DECIMAL(8,2)	NOT NULL DEFAULT 0.1,
	prod_desc	VARCHAR(1000)	NULL
)
```



