---
title: mysql格式化日期
date: 2019-01-31 12:39:29
categories: "mysql"
tags: ["mysql", "date_format"]
---

# mysql格式化日期
mysql查询记录如果有时间戳字段时，查看结果不方便，不能即时看到时间戳代表的含义，现提供mysql格式换时间函数，可以方便的看到格式化后的时间。
## 1.DATE_FORMAT() 函数用于以不同的格式显示日期/时间数据。
```
DATE_FORMAT(date,format)
```
format参数的格式有

|参数|说明|
|----|---|
|%a|缩写星期名
|%b|缩写月名
|%c|月，数值
|%D|带有英文前缀的月中的天
|%d|月的天，数值(00-31)
|%e|月的天，数值(0-31)
|%f|微秒
|%H|小时 (00-23)
|%h|小时 (01-12)
|%I|小时 (01-12)
|%i|分钟，数值(00-59)
|%j|年的天 (001-366)
|%k|小时 (0-23)
|%l|小时 (1-12)
|%M|月名
|%m|月，数值(00-12)
|%p|AM 或 PM
|%r|时间，12-小时（hh:mm:ss AM 或 PM）
|%S|秒(00-59)
|%s|秒(00-59)
|%T|时间, 24-小时 (hh:mm:ss)
|%U|周 (00-53) 星期日是一周的第一天
|%u|周 (00-53) 星期一是一周的第一天
|%V|周 (01-53) 星期日是一周的第一天，与 %X 使用
|%v|周 (01-53) 星期一是一周的第一天，与 %x 使用
|%W|星期名
|%w|周的天 （0=星期日, 6=星期六）
|%X|年，其中的星期日是周的第一天，4 位，与 %V 使用
|%v|年，其中的星期一是周的第一天，4 位，与 %v 使用
|%Y|年，4 位
|%y|年，2 位

例子：
```
DATE_FORMAT(NOW(),'%b %d %Y %h:%i %p') 
DATE_FORMAT(NOW(),'%m-%d-%Y')  
DATE_FORMAT(NOW(),'%d %b %y')  
DATE_FORMAT(NOW(),'%d %b %Y %T:%f') 
```

## 2. MySQL 格式化函数 FROM_UNIXTIME()

```
SELECT FROM_UNIXTIME(date, '%Y-%c-%d %h:%i:%s' ) as post_date ,   
date_format(NOW(), '%Y-%c-%d %h:%i:%s' ) as post_date_gmt   
FROM `article`  where outkey = 'Y' 
```

### 1、FROM_UNIXTIME( unix_timestamp ) 
参数：一般为10位的时间戳，如:1417363200 
返回值：有两种，可能是类似 'YYYY-MM-DD HH:MM:SS' 这样的字符串，也有可能是类似于 YYYYMMDDHHMMSS.uuuuuu 这样的数字，具体返回什么取决于该函数被调用的形式。

### 2、FROM_UNIXTIME( unix_timestamp ，format ) 
参数 unix_timestamp ：与方法 FROM_UNIXTIME( unix_timestamp ) 中的参数含义一样； 
参数 format : 转换之后的时间字符串显示的格式; 
返回值：按照指定的时间格式显示的字符串；

