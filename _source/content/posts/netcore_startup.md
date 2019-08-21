---
title: "Net面試題"
date: 2019-08-16T16:13:11+08:00
draft: true
toc: false
images:
tags:
  - .NetCore
---


.Net interview
===

## String & string
* string 為 String 的別名，兩者在Compile上並無差別
* 繼承時，必須使用別名

## Stack & Heap
* stack 為靜態配置，不同執行緒使用不同stack
* heap 為動態配置，不同執行緒使用相同heap

## Reference type & Value type
* String is Reference type
* Value type use stack only
* Reference type use **Stack** as variable address but point to object in **Heap**

## ref & out
* ref 需要在執行前初始化參數(給值)
* out 是在程式結束前需要初始化參數(給值)
* ref 可以看成 y 指向 i，所以y的操作就都是在改i
```
int i = 5;
Func(ref i);
//i = 10

public void Func (int y){
    y = 10
}
```

[reference type with ref](https://dotblogs.com.tw/jackeir/2015/06/22/151626)
[stack & heap pic](https://dotblogs.com.tw/jackeir/2015/06/22/151626)

## Class & Struct
* struct is value type
* class is reference type
* struct 不可有無參數的ctor，struct不須new()

## Float, Double & Decimal
* Float - 7 digits (32 bit)
* Double - 15-16 digits (64 bit)
* Decimal - 28-29 significant digits (128 bit)

## IEnumerable & IQueryable
* IQueryable(T) 是給資料庫廠商實作的查詢(Linq to Entities)，用來產生資料庫語法，會在資料庫進行操作
* IEnumerable(T) 是操作記憶體的查詢(Linq to Objects)
[參考](https://dotblogs.azurewebsites.net/kevin_date/2017/09/20/104713)

## delegate & event
* Event += 在Event被觸發時會呼叫的委派function
* 委派function，參數及回傳必須與delegate相同
```
public class Calculator{
    public delegate void Sum();
    public event Sum SumEvent;
    public void Trigger(){
        SumEvent();
    }
}

public static void Main(string[] args){
    Calculator c = new Calculator();
    c.SumEvent += new Calculator.Sum(()=>Console.WriteLine("1 + 1 = 2"));
    c.SumEvent += new Calculator.Sum(()=>Console.WriteLine("2 + 2 = 4"));
    c.SumEvent += new Calculator.Sum(()=>Console.WriteLine("4 + 4 = 8"));
    c.Trigger();
}
```

## Visual Studio Code
[Hotkey](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf)
