---
title: 使用TinyORM連接DB
tags: tinyorm
date: 2017-04-25 15:51:25
---


[TinyORM](https://github.com/sdrapkin/SecurityDriven.TinyORM/wiki/Quick-start)
是前幾天看到 This week in .Net介紹的新的ORM Framework

想說挺有趣的，就跟著Wiki在.Net 4.5.2搭配localdb做了個demo

# **基本的查詢指令**

```csharp
var db = DbContext.CreateDbContext
            ("Data Source=(localdb)\\mssqllocaldb;;Initial Catalog=tempdb;" +
             "Integrated Security=True;Pooling=true;Max Pool Size=3000;");
var rows = db.QueryAsync("select [Answer] = 2 + 3").Result;

Console.WriteLine(rows[0].Answer);      //用欄位名稱取值
Console.WriteLine(rows[0]["Answer"]);   //用欄位名稱取值
Console.WriteLine(rows[0][0]);          //用欄位Index取值
```

結果：
{% asset_img img01.png [執行結果] %}  

# **對應到已存在的類別**

```csharp
public class POCO
{
    public int Answer { get; set; }
}
```

```csharp
// 只需要撈弟一筆紀錄的狀況
var rows = db.QueryAsync("select [Answer] = 2 + 3").Result;
var poco = (rows[0] as RowStore).ToObject<POCO>();
var pocoViaFactory = (rows[0] as RowStore).ToObject(() => new POCO());
Console.WriteLine(poco.Answer); // 5
Console.WriteLine(pocoViaFactory.Answer); // 5
```

{% asset_img img02.png [執行結果] %}  

```csharp
// 要撈出所有object id
var ids = db.QueryAsync("select [Answer] = object_id from sys.objects;").Result;
var pocoArray = ids.ToObjectArray<POCO>();
var pocoArrayViaFactory = ids.ToObjectArray(() => new POCO());
for (var i = 0; i < pocoArray.Length; ++i) Console.WriteLine(ids[i].Answer);
Console.WriteLine(string.Empty); // 故意印一行空白分隔上下執行結果
for (var i = 0; i < pocoArrayViaFactory.Length; ++i) Console.WriteLine(ids[i].Answer);
```

{% asset_img img03.png [執行結果] %}

# **參數化查訊搭配匿名物件**

```csharp
var ids1 = db.QueryAsync(
    "select [Answer] = object_id from sys.objects where object_id between @low and @high;",
    new { @low = 10, @high = 40 }).Result;
foreach (var ids in ids1)
{
    Console.WriteLine(ids.Answer);
}
```

{% asset_img img04.png [執行結果] %}

# **參數化查訊搭配Where In**

```csharp
// 請讓我偷懶不截查詢結果了XD
var ids2 = db.QueryAsync(
    "select [Answer] = object_id from sys.objects where object_id in (@range)",
    new { @range = Enumerable.Range(1, 40) }).Result;
```

# **參數化查訊條件為NULL**

```csharp
var emptyResult = db.QueryAsync(
    "select [Answer] = object_id from sys.objects where object_id = @id",
    new { @id = default(int?) }).Result; // 或是用 @id = (int?)null
Console.WriteLine("Result Count: " + emptyResult.Count);
foreach (var ids in emptyResult)
{
    Console.WriteLine(ids.Answer);
}
```

{% asset_img img05.png [執行結果] %}

# **參數化查訊搭配Dictionary**

```csharp
// 請讓我偷懶不截查詢結果了XD
var parameters = new Dictionary<string, object> { { "@low", 10 }, { "@high", 40 } };
var idsDict = db.QueryAsync(
    "select [Answer] = object_id from sys.objects where object_id between @low and @high;",
    parameters).Result;
foreach (var ids in idsDict)
{
    Console.WriteLine(ids.Answer);
}
```

# **欄位名稱大小寫是有差別**

```csharp
var rows = db.QueryAsync("select [Answer] = 2 + 3").Result;
Console.WriteLine(rows[0].Answer is FieldNotFound); // False
Console.WriteLine(rows[0].answer is FieldNotFound); // True
```

{% asset_img img06.png [執行結果] %}

# **使用TinyORM提供的RowStore顯示資料**

```csharp
var row = db.QueryAsync("select * from sys.objects").Result.First();
foreach (var column in row)
    Console.WriteLine("[{0}] [{1}]", column.Key, (column.Value ?? "[NULL]").ToString());
```

{% asset_img img07.png [執行結果] %}

# **使用TinyORM提供的RowStore並用row.ToString()顯示資料**

```csharp
var row = db.QueryAsync("select * from sys.objects").Result.First();
Console.WriteLine(row); // 預設會呼叫row.ToString()
```

{% asset_img img08.png [執行結果] %}

# **使用匿名物件接收result**

```csharp
var rows = db.QueryAsync("select top (4) * from sys.objects").Result;
foreach (var row in rows)
    Console.WriteLine(new { Name = (string)row.name, ObjectId = (int)row.object_id });
```

{% asset_img img09.png [執行結果] %}


## Link

* [Quick start - TinyORM](https://github.com/sdrapkin/SecurityDriven.TinyORM/wiki/Quick-start)