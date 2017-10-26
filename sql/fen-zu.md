## 分组数据

使用分组可以将数据分成多个逻辑组，对每个组进行聚集计算。

GROUP BY子句表示要分组数据，然后对每组数据（而不是整个结果集）进行聚集。

例如：返回每个供应商提供的产品数量：

```
SELECT vend_id, COUNT(*) AS num_prods
FROM Products
GROUP BY vend_id;
```

GROUP BY子句使用须知：

* 除了聚集计算语句外，SELECT语句中的每个列都必须在GROUP BY子句中给出；
* 如果分组列中包含具有NULL值的行，则NULL将作为一个分组返回；
* GROUP BY子句必须出现在WHERE子句之后，ORDER BY子句之前；

## 过滤分组

HAVING子句：HAVING非常类似于WHERE，目前为止所学过的所有类型的WHERE子句都可以用HAVING来替代，唯一的差别是：WHERE过滤行，且出现在GROUP BY前面；而HAVING过滤分组，出现在GROUP BY后面。

例如：找出至少有两个订单的所有顾客：

```
SELECT cust_id, COUNT(*) AS orders
FROM Orders
GROUP BY cust_id
HAVING COUNT(*) >= 2；
```

WHERE子句在数据分组前进行过滤，过滤掉的行不包含在分组中；HAVING子句在分组后进行过滤。

例如：列出提供两个商品以上且价格大于等于4的供应商：

```
SELECT vend_id, COUNT(*) AS num_prods
FROM Products
WHERE prod_price >= 4        --排除价格低于4的商品（排除的商品不参与分组）
GROUP BY vend_id
HAVING COUNT(*) >= 2;
```

一般在使用GROUP BY子句时，应该也给出ORDER BY子句，这是保证数据正确排序的唯一方法。

例如：列出订单商品数量大于3的订单及商品数量：

```
SELECT order_num, COUNT(*) AS items
FROM OrderItems
GROUP BY order_num
HAVING COUNT(*) >= 3
ORDER BY items, order_num;
```



