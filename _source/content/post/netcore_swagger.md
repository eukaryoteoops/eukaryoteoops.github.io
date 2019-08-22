---
title: "[.NetCore] Swagger設定"
date: 2019-08-17T08:33:56+08:00
tags:
    - NetCore
---


Swagger 是讓你方便建立符合API規範的說明文件工具，以下將介紹如何在.Net Core的專案下使用Swagger
<!--more-->
## 透過Nuget安裝 Swashbuckle.AspNetCore

## 在 Startup 加入設定
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddSwaggerGen(c =>
    {
        //Tag是拿來分類actions，預設的tag是controller name，可以在此修改想要的分類方式
        c.TagActionsBy((apiDesc) => $"{apiDesc.ActionDescriptor.RouteValues["controller"]}_{apiDesc.HttpMethod}");
        //此排序方式非字面上可以排序每個Actions，因為Swagger的文件架構會以path當作分組的依據，此排序只能生效在同一組path裡面
        c.OrderActionsBy(api => api.HttpMethod);                                                                        
        //忽略含有[Obsolete]的Actions
        c.IgnoreObsoleteActions();                                                                                      
        //忽略含有[Obsolete]的Properties
        c.IgnoreObsoleteProperties();           
        //將Enum轉為文字顯示於介面上，而非數字。                                                                       
        c.DescribeAllEnumsAsStrings();                   
        //若專案內有不同namespace相同名稱的class，此方法可顯示絕對路徑的class name                                                             
        c.CustomSchemaIds(type => type.FullName);                                                   
        //加入xml，完善API的說明          
        c.IncludeXmlComments(Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Api.xml"));     
        //可以自訂義operation的一些參數，像是在有[Authorized]的operation上加上填寫token的欄位                     
        c.OperationFilter<SwaggerAuthFilter>();
        c.SwaggerDoc("v1", new Info { Title = "Project", Version = "v1" });
    });
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    app.UseSwagger();
    app.UseSwaggerUI(opt =>
    {
        opt.SwaggerEndpoint("/swagger/v1/swagger.json", "v1.0.0");
        //摺疊所有分類
        opt.DocExpansion(DocExpansion.None);
        //顯示此要求花費的時長
        opt.DisplayRequestDuration();
        //顯示Action Name
        opt.DisplayOperationId();
    });
}
```

## 讓專案建置時產出XML檔案
+ 開啟專案屬性 > 建置標籤 (若要在其他環境下也使用Swagger，組態方面要選取**所有組態**，以免部屬到其他環境缺少XML而報錯)
+ 底下輸出區塊，XML文件檔案打勾
+ 填入與上一步驟 `c.IncludeXmlComments()`相同的XML檔案名稱
+ 此時建置後，會在專案目錄下產出XML檔案，接著在XML檔案內容 > 複製到輸出目錄，選取永遠複製

## 使用Swagger
設定完畢之後，可以試試偵錯專案，在Url輸入 `http://{yourDebugDomain:port}/swagger` ，就可以看到Swagger的介面囉