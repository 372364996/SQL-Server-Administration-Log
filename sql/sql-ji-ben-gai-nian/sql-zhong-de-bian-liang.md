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

--PRINT @sum;        --PRINT用于显示char类型、varchar类型，以及可以自动转换为字符串类型的其他类型。
SELECT @sum;
GO
```

全局变量：

全局变量是SQL Server 系统提供并赋值的变量，以@@开头，也称配置函数，用于存储系统的特定信息，作用范围并不局限于某一批处理或存储过程，任何批处理或存储过程可随时调用。

* 全局变量是只读的；
* 用户只能使用，不能自己定义全局变量，也不能修改其值；

常用的全局变量：

```
SELECT @@CPU_BUSY;        --SQL Server 自上次启动时的工作时间，单位：毫秒
SELECT @@CURSOR_ROWS;     --打开上一个游标中当前限定行的数目；
SELECT @@ERROR;           --上一条 T-SQL 语句中报告的错误号；
SELECT @@IDENTITY;        --最后插入的标识值；
SELECT @@LANGID;          --当前使用的语言ID；
SELECT @@NESTLEVEL;       --当前存储过程的嵌套级别（初始值0）
SELECT @@PROCID;          --T-SQL 当前模块的id；
SELECT @@ROWCOUNT;        --上一条 T-SQL 语句影响的行数；
SELECT @@SERVERNAME;      --本地服务器的名字；
SELECT @@SPID;            --当前用户进程的会话ID；
SELECT @@VERSION;         --当前SQL Server 的版本、处理器体系结构、生成日期；
```



