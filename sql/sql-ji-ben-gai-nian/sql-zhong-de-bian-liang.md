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
		@sum int

SET @i = 50
SET @j = 60
SELECT @sum = @i + @j

--PRINT @sum
SELECT @sum
GO
```

全局变量：

