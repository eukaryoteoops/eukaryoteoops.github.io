---
title: "[Linq] Aggregate"
date: 2019-08-30T08:33:56+08:00
tags:
    - Linq
---

1. **無初始值的累加函式**
```
public static TSource Aggregate<TSource> (
    this IEnumerable<TSource> source, 
    Func<TSource,TSource,TSource> func);
```
+ 例如Sum()這個函式，就可以用Aggregate來實作
```
List<int> list = new List<int>{1, 2, 3};
var result = list.Aggregate((aggregatedSoFar, nextElement) => nextElement + aggregatedSoFar);
// 1. (0, 1) => 0 + 1 
// 2. (1, 2) => 2 + 1
// 3. (3, 3) => 3 + 3
//result = 6
```
+ 每次的`nextElement + aggregatedSoFar`都會丟回`aggregatedSoFar`，進行下一次的運算
2. **有初始值的累加函式**
```
public static TAccumulate Aggregate<TSource,TAccumulate> (
    this IEnumerable<TSource> source, 
    TAccumulate seed, 
    Func<TAccumulate,TSource,TAccumulate> func);
```
+ 與*無初始值的累加函式*不同的是，會將初始值放進`aggregatedSoFar`作為初始的運算
```
List<int> list = new List<int>{1, 2, 3};
var result = list.Aggregate(20, (aggregatedSoFar, nextElement) => nextElement + aggregatedSoFar);
// 1. (20, 1) => 1 + 20 
// 2. (21, 2) => 2 + 21
// 3. (23, 3) => 3 + 23
//result = 26
```
3. **有初始值的累加函式，且多使用一個 Func作為最終結果的處理**
```
public static TResult Aggregate<TSource,TAccumulate,TResult> (
    this IEnumerable<TSource> source,
    TAccumulate seed,
    Func<TAccumulate,TSource,TAccumulate> func,
    Func<TAccumulate,TResult> resultSelector);
```
+ 將最後的結果，做處理之後才回傳
```
List<int> list = new List<int>{1, 2, 3};
var result = list.Aggregate(20, (aggregatedSoFar, nextElement) => nextElement + aggregatedSoFar, final => final + 10);
// 1. (20, 1) => 1 + 20 
// 2. (21, 2) => 2 + 21
// 3. (23, 3) => 3 + 23
// final. 26 => 26 + 10
//result = 36
```

[msdn](https://docs.microsoft.com/zh-hk/dotnet/api/system.linq.enumerable.aggregate?view=netframework-4.8)