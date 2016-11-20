---
title: 'Using NuGet in Script CSharp'
date: 2016-10-27 19:52:28
tags: C#
---

假設現在我們要從NuGet安裝[Json.Net](https://www.nuget.org/packages/Newtonsoft.Json/)

```bash
scriptcs -install Newtonsoft.Json -p 8.0.3
```

`-p` 表示指定版本  

要特別指定是有原因的  
之前測試時，不指定版本(預設9.0.1)後，發現無法安裝  
會跳出`InavlidOperationException`  
上網查資料後，有人講到指定版本到8.0.3就可以安裝  
據說是跟Nuget有關就是，希望之後會修正@@"

新增一個app.csx，內容如下：

```C#
using Newtonsoft.Json;
var product = new {Name = "Apple", Size = "Small"};
Console.WriteLine(JsonConvert.SerializeObject(product));
```

這時候畫面就會跑出
```bash
{"Name":"Apple","Size":"Small"}
```

就跟我們平常寫C#的程式一樣  
很神奇吧～

## Link

* [scriptcs.net](http://scriptcs.net/)