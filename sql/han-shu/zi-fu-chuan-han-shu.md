## 字符串函数

对字符串执行操作，并返回字符串或数值。字符串函数是标量函数。

```
SELECT ASCII('abc');        --返回最左端（a字符）的ASCII码值（97）
SELECT CHAR(97);            --返回ASCII码值代表的字符(a)
SELECT UNICODE(N'数据库');   --返回给定字符串最左端（数）的Unicode码值(25968)
SELECT NCHAR(25968);        --返回Unicode码值代表的字符（数）
SELECT CHARINDEX('a','what are you doing?',1);    --返回从位置1开始（默认位置为1）在字符串（'what are you doing?'）中
                                                  --查找字符（a）首次出现的位置。（3）
SELECT SOUNDEX('what');     --返回字符串的发音表示的四字符代码，用来比较两个字符串发音是否匹配(W300)
SELECT DIFFERENCE('height','hit');    --返回两个字符串发音表示的四字符代码的差值(3)
SELECT LEFT('abcdefg',4);   --从左边开始截取4位长度的字符串（abcd）
SELECT RIGHT('abcdefg',4);  --从右边开始截取4位长度的字符串（defg）
SELECT REPLICATE('ab-',5);  --将给定字符串重复5次后返回（ab-ab-ab-ab-ab-）
SELECT REVERSE('abcdefg');  --翻转字符串（gfedcba）
SELECT STR(12345.6789,12,2);	--将float类型数据转换为总位数12（不够在前面补空格）、小数位数为2位的字符串（    12345.68）
SELECT SPACE(5);				--返回由5个空格组成的字符串(     )
SELECT STUFF('abcdefg',2,3,'*');	--用字符*替换abcdefg字符串中从位置2开始长度为3个字符，并返回（a*efg）
SELECT LEN('abc  ');			--返回字符串的字节数，不包含尾随的空格（3）
SELECT LOWER('ABC');			--转换小写(abc)
SELECT UPPER('abc');			--转换大写(ABC)
SELECT PATINDEX('%ab%','acvmvmvvabcvmvvmmab');		--返回模式%ab%在字符串acvmvmvvabcvmvvmmab中第一次匹配的起始位置，不匹配返回0（9）
SELECT SUBSTRING('abcdefg',2,3);	--截取字符串，从位置2开始截取长度为3的字符串（bcd）
```



