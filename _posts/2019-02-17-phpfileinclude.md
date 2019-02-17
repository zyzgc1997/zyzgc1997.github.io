---
layout: post
title: 'php文件包含漏洞'
date: 2019-2-17
author: hackz
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-banner.png'
tags: web漏洞 文件包含
---
# php文件包含漏洞

## php中引发文件包含漏洞的通常是以下四个函数：
1. include()
2. include_once()
3. require()
4. require_once()

### include()&require()
> require()

在包含的过程中如果遇到错误，比如文件不存在等，则会直接退出，不执行后续语句。
![require_test](https://github.com/zyzgc1997/zyzgc1997.github.io/tree/master/assets/img/require_test.png)

> include()

在包含的过程中如果遇到错误，即使文件不存在等，也不会直接退出，会继续执行后续语句。
![include_test](https://github.com/zyzgc1997/zyzgc1997.github.io/blob/master/assets/img/include_test.png)

### require_once()&include_once()
`require_once()` 和 `include_once()` 功能与require() 和 include() 类似。但如果一个文件已经被包含过了，则 require_once() 和 include_once() 则不会再包含它，以避免函数重定义或变量重赋值等问题。

### 当利用这四个函数来包含文件时，不管文件是什么类型（图片、txt等等），都会直接作为php文件进行解析。测试代码：
```
include_test.php?file=phpinfo.txt
```
在同目录下的phpinfo.txt文件如下
```
<?php
	phpinfo();
?>
```
可成功解析phpinfo()
![phpinfo_test](https://github.com/zyzgc1997/zyzgc1997.github.io/blob/master/assets/img/phpinfo_test.png)

