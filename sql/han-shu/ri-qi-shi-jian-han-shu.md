## 日期时间函数

对日期和时间执行操作，日期时间函数是标量函数。

用来获取系统日期和时间值的函数：

```
SELECT SYSDATETIME();		--返回包含系统日期和时间的datetime2值（2017-11-03 09:35:57.8236814）
SELECT SYSDATETIMEOFFSET();	--返回包含系统日期和时间的datetimeoffset值（2017-11-03 09:36:50.5447126 +08:00）
SELECT SYSUTCDATETIME();	--返回包含系统日期和时间的datetime2值，日期和时间作为UTC时间返回（2017-11-03 01:38:01.1152090）
SELECT CURRENT_TIMESTAMP;	--返回系统当前的日期和时间的datetime2值（2017-11-03 09:40:53.130）
SELECT GETDATE();			--返回系统日期和时间的datetime2值（2017-11-03 09:41:09.557）
SELECT GETUTCDATE();		--返回系统日期和时间的UTC值（2017-11-03 01:42:19.200）
```



