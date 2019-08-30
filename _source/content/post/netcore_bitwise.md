---
title: "[.NetCore] 位元運算子"
date: 2019-08-29T08:33:56+08:00
tags:
    - NetCore
---

## complement operator [~]
+ 會反轉位元
+ 負數的位元表示法是用二補數的方式，舉個例子
    1. 6 > 0110
    2. 反轉位元 > 1001
    3. 加上1成為負數 > 1010
    4. 1010 就是 -6 的表示法
+ 為啥 1010 不是 10 呢 > 偷懶了，以int32來說他的完整表示法是 1111 1111 1111 1111 1111 1111 1111 1010

```C#
int i = 5;  // 0101
int j = ~i; // 1010 < 這貨就是-6
//j = -6
```
+ 若是uint就沒有負數了
```C#
uint i = 5;     //0000 0000 0000 0000 0000 0000 0000 0101
uint j = ~i;    //1111 1111 1111 1111 1111 1111 1111 1010
//j = 4294967290
```

## Left-shift operator [<<]
+ 將每個位元向左移指定的位元數，後方補0
```C#
int i = 9; //1001
int j = i << 2
// j = 36 -> 100100
```
實際上等於是做了乘法，每左移一個位元，就會乘2
` 9 * 2 * 2 = 36 `

## Right-shift operator [>>]
+ 將每個位元向右移指定的位元數，前方補0
```C#
int i = 9; //1001
int j = i >> 2
// j = 2 -> 0010
```
實際上等於是做了除法，每左移一個位元，就會除2，取商數，捨餘數
` Math.Abs(9/2/2) = 2 `

## Logical AND operator [&]
|first unit|second unit|AND result|
|:-:|:-:|:-:|
|1|1|1|
|1|0|0|
|0|1|0|
|0|0|0|

```C#
int a = 9;
a &= 1; //a = a & 1;
//a = 1001 & 0001 = 0001 = 1(int)
```
## Logical OR operator [|]
|first unit|second unit|OR result|
|:-:|:-:|:-:|
|1|1|1|
|1|0|1|
|0|1|1|
|0|0|0|

```C#
int a = 9;
a |= 2; //a = a | 2;
//a = 1001 | 0010 = 1011 = 11(int)
```

## Logical exclusive OR operator [^]
|first unit|second unit|XOR result|
|:-:|:-:|:-:|
|1|1|0|
|1|0|1|
|0|1|1|
|0|0|0|

```C#
int a = 9;
a ^= 3; //a = a ^ 3;
//a = 1001 ^ 0011 = 1010 = 10(int)
```

## ref
+ [msdn](https://docs.microsoft.com/zh-tw/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators)
+ [blog](https://dotblogs.com.tw/feegg333/2011/06/22/29525)
+ [二補數](https://noob.tw/complements/)