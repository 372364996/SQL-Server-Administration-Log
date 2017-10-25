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



