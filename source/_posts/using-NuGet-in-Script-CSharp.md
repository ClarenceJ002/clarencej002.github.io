---
title: 'Using NuGet in Script CSharp'
date: 2016-10-27 19:52:28
tags: C#
---

假設現在我們要從NuGet安裝[Json.Net](https://www.nuget.org/packages/Newtonsoft.Json/)

```bash
scriptcs -install Newtonsoft.Json
```

新增一個app.csx，內容如下：

```C#
var product = new {Name = "Apple", Size = "Small"};
Console.WriteLine(JsonConvert.SerializeObject(product));
```


## Link

* [script cs](http://scriptcs.net/)