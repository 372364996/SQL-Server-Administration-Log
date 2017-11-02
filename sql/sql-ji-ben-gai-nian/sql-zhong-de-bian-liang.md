## 变量

变量是在程序运行过程中发生改变的量。根据作用范围，可将变量分为局部变量和全局变量。

局部变量：

局部变量是用户自己定义的变量，用于在批处理或存储过程中保存值的变量。局部变量必须先声明后使用，初始值为NULL，局部变量使用DECLARE来声明：

```
DECLARE @name varchar(8);
```

为局部变量赋值（两种方式都可以）：

```
SET @name = 'WANG';    -- 每次给一个变量赋值
SELECT @name = 'WANG'    -- 每次可以同时给多个变量赋值
```

例如：编写程序计算两个数之和：

```
DECLARE @i int,
        @j int,
        @sum int;

SET @i = 50;
SET @j = 60;
SELECT @sum = @i + @j;

--PRINT @sum;        --打印输出110
SELECT @sum;         --返回单个单元格，值为110
GO
```

全局变量：

全局变量是SQL Server 系统提供并赋值的变量，以@@开头，也称配置函数，用于存储系统的特定信息，作用范围并不局限于某一批处理或存储过程，任何批处理或存储过程可随时调用。

* 全局变量是只读的；
* 用户只能使用，不能自己定义全局变量，也不能修改其值；

常用的全局变量：

```


SELECT @@CPU_BUSY;
SELECT @@CURSOR_ROWS;
SELECT @@ERROR;
SELECT @@IDENTITY;
SELECT @@LANGID;
SELECT @@NESTLEVEL;
SELECT @@PROCID;
SELECT @@ROWCOUNT;
SELECT @@SERVERNAME;
SELECT @@SPID;
SELECT @@VERSION;
```



