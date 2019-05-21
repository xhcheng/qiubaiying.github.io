---
layout:     post                           # 使用的布局（不需要改）
title:      深入理解MySQL                     # 标题
subtitle:   MySQL原理与优化                   #副标题
date:       2019-05-19                      # 时间
author:     小虫子                           # 作者
header-img: img/post-bg-debug.png            #这篇文章标题背景图片
catalog: false                               # 是否归档
tags:                                        #标签
    - MySQL
---


## MySQL体系结构
![MySQL体系结构图](/img/mysql-structure.png)

**1.Connectors：**不同语音中与sql的交互，简单说就是接口客户端。

**2.Management Serveice & Utilities：**系统管理和控制工具mysql、mysqldump等，用来管理数据库，备份，恢复，安全控制等等。

**3.Connection Pool：**连接池，管理缓冲用户连接，线程处理等需要缓存的需求。

**4.SQL Interface：**sql接口，接受用户sql命令，并返回用户要查询的结果。

**5.Parser：**解析器，sql命令传输到解析器的时候会被解析器验证和解析。主要功能：
* a.将sql语句分解成数据结构，并将这个结构传输到后续步骤，以后sql语句的传递和处理就是基于这个结构的。
* b.如果在分解构成中遇到错误，那么就说明这个sql语句是不合理的。

**6.optimizer：**查询优化器

sql语句在执行之前会使用查询优化器对查询进行优化。他使用的是“选取-投影-联接”策略进行查询。用一个例子可以理解：select uid,name form user where gender=1；这个select查询先根据where语句进行选取，而不是先将全表查出来以后再进行gender过滤。这个select查询先根据uid和那么属性投影，而不是将属性全部取出后再进行过滤。最后将这两个查询条件联接起来生成最终查询结果。

**7.Cache和Buffer：**查询缓存
**8.Engine：**存储引擎

存储引擎是MySQL中具体与文件打交道的子系统，也是MySQL最具特色的一个地方。MySQL的存储引擎是插入式的，它根据MySQL AB公司提供的文件中间访问层的一个抽象接口来定制一种文件访问机制（这种访问机制就叫存储引擎）。现在有很多种存储引擎，各个存储引擎的优势各不一样，最常用的 MyISAM，InnoDB。


MySQL表存储引擎

PHP的MySQL驱动和API

MySQL索引

sql语句优化和性能调优