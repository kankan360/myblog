---
title: 自己常用的一些mysql
date: 2019-01-31 14:18:34
categories: "mysql"
tags: "mysql"
---

# 自己常用的一些mysql操作

## 1、把当天出票时间转unix时间戳到某排序字段，方便程序排序
```
BEGIN
update jw_items AS jw set jw.chupiao_top = 0;
update jw_items AS jw set jw.chupiao_top = unix_timestamp(jw.quchendate) WHERE (jw.chupiaodate = DATE_FORMAT(now(),'%Y/%c/%e')) AND ishidden <> 1;
END
```

## 2、定时检测付款状态把未按设置时间段的订单重置
```
update jw_orders od,jw_config conf,jw_items jw set od.paystate = 3 WHERE (from_unixtime(od.ordertime + conf.order_keeptime*3600) <= NOW()) AND (od.ordertime > 0) AND (jw.id = od.itemsid) AND (od.paystate IN (1,2))
```

## 3、把相关字段日期字符转unix时间戳
```
unix_timestamp(xxx_field)
```
## 4、把字符串日期格式加一天并更新
```
UPDATE tables SET field = date_format(DATE_ADD(STR_TO_DATE(field,'%Y/%c/%e'),INTERVAL 1 DAY),'%Y/%c/%e') WHERE id = xxx
```

## 5、保留七天日志
```
DELETE FROM jw_tablesxxx WHERE op_time < (UNIX_TIMESTAMP(DATE_FORMAT(NOW(),'%Y-%m-%d')) - 604800)
```

## 6、 删除无关系操作日志
```
DELETE tb_a FROM jw_xxxx_logs as tb_a INNER JOIN(SELECT jw_xxxx_logs.id FROM jw_items RIGHT JOIN jw_xxxx_logs on jw_xxxs.id = jw_xxxx_logs.jwid WHERE jw_xxxs.id IS NULL) as tb_b on tb_b.id = tb_a.id
```

......
> 未完等补充