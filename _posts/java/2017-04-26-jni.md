---
layout: post
title: JNI
date: 2017-04-26 17:33:17 +0800
category : 技术文档
tag :
- java
- jni
---
* content
{:toc}

#### Java通过JNI机制和C/C++沟通的具体步骤

1. 编写包含native本地方法的java类
2. 通过javah工具生成C/C++语言的头文件
3. 使用C/C++语言实现头文件
4. 使用交叉编译工具对C/C++本地代码进行编译，最后通过链接生成*.so可执行的C/C++库
5. 实际执行Java代码去和本地的C/C++代码互相沟通


