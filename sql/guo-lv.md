## 使用WHERE子句

SQL过滤与应用过滤：建议在SQL中过滤数据，可以更快速；而且节省网络带宽。

WHERE子句的位置：WHERE子句位于FROM子句后面，ORDER BY子句前面。

```
SELECT prod_name, prod_price
FROM Products
WHERE prod_price = 3.49
```

## WHERE子句操作符

| 操作符 | 说明 | 操作符 | 说明 |
| :---: | :--- | :---: | :--- |
| = | 等于 | &gt; | 大于 |
| &lt;&gt; | 不等于 | &gt;= | 大于等于 |
| != | 不等于 | !&gt; | 不大于 |
| &lt; | 小于 | BETWEEN......AND...... | 在指定的两个值之间 |
| &lt;= | 小于等于 | IS NULL | 为NULL的值 |
| !&lt; | 不小于 | IN | 指定条件范围内的任何值都可以进行匹配 |

## 不匹配检查

无法返回vend\_id 为NULL的列，因为未知（unknown）具有特殊的含义，数据库不知道它是否匹配。

```
SELECT vend_id, prod_name
FROM Products
WHERE vend_id <> 'DLL01'
```

## 范围检查

BETWEEN关键字，必须指定两个值——所需范围的低端值和高端值，这两个值必须用AND分隔。

```
SELECT prod_name, prod_price
FROM Products
WHERE prod_price BETWEEN 5 AND 10
```

## 空值检查

在一个列不包含值时，称其包含空值NULL。在创建表时，可以指定列是否能不包含值。

```
SELECT cust_name
FROM Customers
WHERE cust_email IS NULL
```

## 组合WHERE子句

AND操作符：

要通过不止一个列进行过滤。

```
SELECT prod_id, prod_name, prod_price
FROM Products
WHERE vend_id = 'DLL01'
AND prod_price <= 4
```

OR操作符：

检索匹配任意条件的行。

```
SELECT prod_name, prod_price
FROM Products
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01'
```

## 求值顺序

WHERE子句允许包含任意多个AND和OR操作符，允许两者结合起来进行复杂、高级的过滤。

SQL在处理OR操作符前，优先处理AND操作符。例如：想要列出价格10美元以上，且有DLL01和BRS01制造的所有产品：

```
SELECT prod_name, prod_price
FROM Products
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01' AND prod_price >= 10
```

这条语句实际翻译为：由供应商BRS01制造的且价格为10美元以上的所有产品，加上由供应商DLL01制造的所有产品。

解决方案：使用圆括号。因为圆括号具有不AND和OR更高的求值顺序。

```
SELECT prod_name, prod_price
FROM Products
WHERE (vend_id = 'DLL01' OR vend_id = 'BRS01')
AND prod_price >= 10
```

## IN操作符

用来指定条件范围，由逗号分隔，扩在圆括号中的条件，每个条件都可以进行匹配。功能与OR相当。

```
SELECT prod_name, prod_price
FROM Products
WHERE vend_id IN ('DLL01', 'BRS01')
ORDER BY prod_name;
```

使用IN操作符的优点：

* 在有很多合法选项时，IN操作符的语法更清楚；
* 在与其他AND和OR操作符组合使用时，使用IN操作符使求值顺序更容易管理；
* IN操作符一般**比一组OR操作符执行的更快**。
* IN的**最大优点是可以包含其他SELECT语句**，能够更动态的建立WHERE子句。

## NOT操作符

WHERE子句中用来否定其后所跟的任何条件的关键字。

例如：取出除DLL01之外的所有供应商制造的产品：

```
SELECT prod_name
FROM Products
WHERE NOT vend_id = 'DLL01'
ORDER BY prod_name;
```

NOT关键字与IN关键字联合使用时，可以非常简单的找出与条件列表不匹配的行。

## LIKE操作符

LIKE指示后面跟的搜索模式利用通配符而不是简单的相等匹配进行比较。为了在搜索子句中使用通配符，**必须使用LIKE操作符**。

通配符搜索**只能用于文本字段**（字符串），非文本数据类型字段不能使用通配符搜索。使用通配符是由代价的，即通配符搜索一般比其他搜索要消耗更长的处理时间。

使用通配符的技巧：

* 不要过度使用通配符，能使用操作符的尽量使用操作符；
* 不要将通配符置于搜索模式的开始处，因为这样搜索起来是最慢的；
* 仔细斟酌通配符的位置，放错位置则不会返回想要的数据。

百分号（%）通配符：

%表示任意字符出现任意次数（0次、1次或多次）。但有一个例外，不会匹配值为NULL的行。

例一：找出所有以Fish开头的产品：

```
SELECT prod_id, prod_name
FROM Products
WHERE prod_name LIKE 'Fish%';
```

通配符可以在搜索模式中的任意位置使用，并且可以使用多个。

例二：找出产品名称包含bean bag的产品：

```
SELECT prod_id, prod_name
FROM Products
WHERE prod_name LIKE '%bean bag%';
```

通配符可以出现在搜索模式的中间。

例三：找出所有以F开头、以y结尾的所有产品：

```
SELECT prod_id, prod_name
FROM Products
WHERE prod_name LIKE 'F%y';
```

下划线（\_）通配符：

\_只匹配单个字符。

```
SELECT prod_id, prod_name
FROM Products
WHERE prod_name LIKE '__ inch teddy bear';
```

方括号（\[\]）通配符：

\[\]用来指定一个字符集，它必须匹配**指定位置**的**单个**字符。

例一：找出以J和M开头的联系人：

```
SELECT cust_contact
FROM Customers
WHERE cust_contact LIKE '[JM]%'
ORDER BY cust_contact;
```

此通配符可以使用前缀字符^（脱字号）来表示否定。

