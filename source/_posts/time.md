---
title: Typecho添加页面生成时间
date: 2022-07-12 09:25:00
author: 雨後
top: false
hide: false
cover: false
toc: false
categories: Typecho
tags:
  - Typecho
---

# 定义
在主题里的functions.php文件添加下面一段代码
```
/**
* 加载时间
* @return bool
*/functiontimer_start(){global$timestart;$mtime=explode(' ',microtime());$timestart=$mtime[1]+$mtime[0];returntrue;}timer_start();functiontimer_stop($display=0,$precision=3){global$timestart,$timeend;$mtime=explode(' ',microtime());$timeend=$mtime[1]+$mtime[0];$timetotal=number_format($timeend-$timestart,$precision);$r=$timetotal<1?$timetotal*1000." ms":$timetotal." s";if($display){echo$r;}return$r;}
```
# 调用

```
加载耗时：<!?php echotimer_stop();?>
```