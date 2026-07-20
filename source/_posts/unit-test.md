---
title: 简单谈谈UnitTest
slogan: "Let's talk about UnitTest"
author: MrKeanu
categories:
  - Incessant Coding-编程不辍
index_img: /image/bg/flower_in_sky.jpg
banner_img: /image/bg/flower_in_sky.jpg
banner_img_height: 70
banner_mask_alpha: 0.3
date: 2025-10-14 22:55:18
subtitle: "Let's talk about UnitTest"
excerpt: "UnitTest简称UT，即单元测试，常常被开发者所嫌讳。本文谈谈UT的启发、作用，以及现有的单元测试框架的使用。"
tags: [架构设计, 软件工程]
archive:
hide:
math: false
mermaid: true
---

UnitTest简称UT，即单元测试，但却常常被开发者所嫌讳。本文从UT的启发、重要性、作用先介绍UT，然后以GoogleTest为例谈谈现有的单元测试框架的使用。

# Unit-Test

## Oh, so this is Unit-Test

单元测试的定义海了去，我也无意在{% label success @“茴香豆的有几种写法”%}上较真，此处直接贴一个Wikipedia的解释[Wiki-单元测试](https://zh.wikipedia.org/zh-cn/%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)。无论它叫**单元测试**还是**模块测试**，第一性原理不可违背，它只做一件事——对代码进行测试。对此再加一个限定，对代码（或者说程序）的最小可测试单元进行，so this is Unit-Test。



{% mermaid %}

graph TD
    A[Test Runner 测试运行器] -->|组织与执行| B[Test Suite 测试套件]
    B -->|包含| C[Test Case 测试用例]
    C -->|使用| D[Assertions 断言]
    C -->|可选使用| E[Test Fixtures 测试夹具]
    A -->|生成| F[测试报告]

{% endmermaid %}

## Wait,  Why do developers need Unit-Test?

重要性，。回到题目，尽管不至于unit-test is all you need，但至少单元测试是一个大型的成功的商业软件不可缺少的一部分。



# GoogleTest





[GoogleTest官方文档](https://google.github.io/googletest/)
