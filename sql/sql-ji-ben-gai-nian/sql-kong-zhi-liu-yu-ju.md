## 控制流语句

控制流语句是指那些用来控制程序执行和流程分支的命令。包括BEEGIN...END、IF...ELSE、CASE、WHILE、CONTINUE、BREAK、GOTO、WAITFOR。

BEEGIN...END语句：

将多个 T-SQL 语句合并成一个语句块，并视为一个单元来处理，允许嵌套。

```
BEGIN
-- 任何有效的 T-SQL 语句或语句块
END
```

IF...ELSE语句：

用来判断当条件成立时执行的程序段，以及条件不成立时执行的程序段，允许嵌套。



```
IF 条件表达式（返回TRUE或FALSE）
-- 条件成立时执行
[ELSE
-- 条件不成立时执行
]
```

CASE语句：

用于计算条件列表，将其中一个符合条件的结果表达式返回，按照使用形式的不同又分为简单CASE函数和搜索CASE函数。

* 简单CASE函数：将输入表达式与一组简单的表达式进行比较：
  ```
  CASE 输入表达式
  WHEN 简单表达式一 THEN 返回表达式
  WHEN 简单表达式二 THEN 返回表达式
  ...
  ELSE 返回表达式        --输入表达式与上面没有匹配时返回
  END
  ```
* 搜索CASE函数：用于计算一组布尔表达式：
  ```
  CASE 
  WHEN 布尔表达式一 THEN 返回表达式
  ...
  ELSE 布尔表达式
  END
  ```

WHILE语句、CONTINUE语句、BREAK语句：

用于循环的 T-SQL 语句。

```
WHILE 条件表达式
-- 程序块
CONTINUE    --用于结束本次循环，回到循环的起点继续执行
-- 程序块
BREAK       --用于跳出循环，结束当前WHILE语句的执行
-- 程序块
```

GOTO语句：

使程序跳到标有标识符的位置继续执行。标识符可以是数字和字母的组合，但必须以冒号（:）结尾。

```
label:
-- 程序块
```

```
GOTO label;
```

WAITFOR语句：

用于暂停 T-SQL 语句的执行，直到所设定的时间已过，才继续执行。

```
WAITFOR
DELAY '等待时间，最长24小时'
| TIME '指定 WAITFOR 语句运行的时间'
```

例如：

```
BEGIN
WAITFOR TIME '7:00'；
EXECUTE 定时工作任务；
END;
GO

```



