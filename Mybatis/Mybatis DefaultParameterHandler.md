---
title: Mybatis -->DefaultParameterHandler跟踪
tags: 'Mybatis,DefaultParameterHandler'
grammar_cjkRuby: true
---

DefaultParameterHandler是Mybatis中给sql中参数赋值的类，其大概过过程如下

1. 通过`boundSql.getParameterMappings()`获取到参数列表
2. 先判断`additionalParameters`列表中是否有这个参数名，如果有就通过参数名取出值，如果没有判断`parameterObject`如果这个参数为`null`就直接返回`null`,否则就只有一个参数的值就这`parameterObject`
3. 通过`parameterMapping`找到`TypeHandler`,通过`TypeHandler` 来给参数赋值
4. 通过`TypeHandler`的`setParameter()`方法，给`PrepareStatment`赋值，其中需要传入的参数是`ps`,是第几个参数，这个顺序是由参数列表中的遍历`i+1`计算出来的，然后是参数
