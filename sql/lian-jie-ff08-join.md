## 关系表

关系表的设计就是要把信息分解成多个表，每个表存储一类信息，各表通过某些共同的值相互关联。

## 联结

联结是一种机制，用来在一条SELECT语句中关联表。

```
SELECT vend_name, prod_name, prod_price
FROM Vendors, Products
WHERE Vendors.vend_id = Products.vend_id
```

WHERE子句的重要性：在联结两个表时，

