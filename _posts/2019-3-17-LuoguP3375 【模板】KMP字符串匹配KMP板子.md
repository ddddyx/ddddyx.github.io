# LuoguP3375 【模板】KMP字符串匹配|KMP|板子


---
layout: post
title: "LuoguP3375 【模板】KMP字符串匹配|KMP|板子"
date: 2019-3-17
excerpt: "在？<br>KK MP？"
tags: [KMP,板子]
comments: true
---


# Problem

> **题目描述**

如题，给出两个字符串s1和s2，其中s2为s1的子串，求出s2在s1中所有出现的位置。

**为了减少骗分的情况，接下来还要输出子串的前缀数组next。**

（如果你不知道这是什么意思也不要问，去百度搜[kmp算法]学习一下就知道了。）

> **输入输出格式**

> 输入格式：

第一行为一个字符串，即为s1

第二行为一个字符串，即为s2

>输出格式：

若干行，每行包含一个整数，表示s2在s1中出现的位置

接下来1行，包括length(s2)个整数，表示前缀数组next[i]的值。

>  **输入输出样例**

>  输入样例#1：

```
ABABABC
ABA
```

>  输出样例#1：

```
1
3
0 0 1 
```

> **说明**

时空限制：1000ms,128M

数据规模：

设s1长度为N，s2长度为M

对于30%的数据：N<=15，M<=5

对于70%的数据：N<=10000，M<=100

对于100%的数据：N<=1000000，M<=1000000

样例说明：

![img](https://cdn.luogu.org/upload/pic/2257.png) 

所以两个匹配位置为1和3，输出1、3

## 分析

显然，KMP板子题。

KMP详解地址(转)：[!转自知乎-我见过最通俗易懂的KMP算法详解]("https://blog.csdn.net/x__1998/article/details/79951598")

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;
const int maxn=1e6+5;
char s1[maxn],s2[maxn];
int nxt[maxn];
void getnxt(char *t){
	nxt[0]=0;
	int n=strlen(t);
	for(int i=1,j=0;i<n;i++){
		while(j&&t[i]!=t[j]) j=nxt[j-1];
		if(t[i]==t[j]) j++;
		nxt[i]=j;
	}
}
void KMP(char *t,char *p){
	int n=strlen(t),m=strlen(p);
	for(int i=0,j=0;i<n;i++){
		while(j&&t[i]!=p[j]) j=nxt[j-1];
		if(t[i]==p[j]) j++;
		if(j==m) printf("%d\n",i-j+2);
	}
}
int main(){
	cin>>s1>>s2;//主串 模式串
	getnxt(s2);
	KMP(s1,s2);
	int n=strlen(s2);
	for(int i=0;i<n;i++) printf("%d ",nxt[i]);
	return 0;
}
```

