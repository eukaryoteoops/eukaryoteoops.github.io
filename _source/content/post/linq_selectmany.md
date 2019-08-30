---
title: "[Linq] SelectMany"
date: 2019-08-29T08:33:56+08:00
tags:
    - Linq
---

+ `SelectMany`可以將序列攤平，使用到兩次foreach的情況，可以考慮用`SelectMany`來簡化寫法

```
class Member
    {
        public int KPI { get; set; }

        public Member(int kpi)
        {
            this.KPI = kpi;
        }
    }

    class Leader
    {
        public string Name { get; set; }

        public List<Member> Members;

        public Leader(string name, List<Member> members)
        {
            this.Name = name;

            this.Members = members;
        }
    }
```
+ 假設有一個集合
```
List<Leader> leader = new List<Leader>{
    new Leader("leaderA", new List<Member>{
        new Member(80),new Member(70)
    }),
    ...
}
```
1. 
```
public static IEnumerable<TResult> SelectMany<TSource,TResult> (
    this IEnumerable<TSource> source,
    Func<TSource,IEnumerable<TResult>> selector);
```

```
List<Member> members = leader.SelectMany(source => source.Members);
```
2. 
```
public static IEnumerable<TResult> SelectMany<TSource,TCollection,TResult> (
    this IEnumerable<TSource> source,
    Func<TSource,IEnumerable<TCollection>> collectionSelector,
    Func<TSource,TCollection,TResult> resultSelector);
```
```
leader.SelectMany(source => source.Members, (source, members) => new {source.Name, members.KPI});
```






[msdn](https://docs.microsoft.com/zh-hk/dotnet/api/system.linq.enumerable.selectmany?view=netframework-4.8)