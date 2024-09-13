## 思维导航

* [EF Core介绍](https://github.com)
* [Entity Framework Plus](https://github.com)
* [项目功能特性](https://github.com)
* [项目NuGet包安装](https://github.com)
* [批量删除](https://github.com)
* [批量更新](https://github.com)
* [查询过滤器](https://github.com)
* [项目源码地址](https://github.com)
* [优秀项目和框架精选](https://github.com)

## EF Core介绍


Entity Framework (EF) Core 是轻量化、可扩展、开源和跨平台版的常用 Entity Framework 数据访问技术，EF Core 是适用于 .NET 的现代对象数据库映射器。它支持 LINQ 查询、更改跟踪、更新和架构迁移。EF Core 通过提供程序插件 API 与 SQL Server、Azure SQL 数据库、SQLite、Azure Cosmos DB、MySQL、PostgreSQL 和其他数据库一起使用（微软官方出品）。


:[MeoMiao 萌喵加速](https://biqumo.org)## Entity Framework Plus


Entity Framework Plus是一个开源、免费（MIT License）、功能强大的 Entity Framework（EF）和 Entity Framework Core（EF Core） 扩展库，旨在提升 Entity Framework 的性能和克服其局限性。通过提供一系列实用的功能，如批量操作、查询缓存、查询延迟、LINQ动态、审计跟踪等，使得使用 Entity Framework 进行数据库开发变得更加高效和灵活。


## 项目功能特性


以下是 `Entity Framework Plus` 项目的一些主要特点和功能：


* **批量操作**：支持批量插入、更新、删除和合并操作，这些操作可以在单个数据库往返中处理多条记录，而无需加载实体到内存中，从而显著提高性能。
* **查询缓存**：提供查询缓存功能，允许将查询结果缓存在内存中，以减少对数据库的重复查询，提高应用程序的响应速度。
* **查询延迟**：允许延迟查询的执行，以便在需要时结合其他功能（如查询缓存和查询未来）一起执行。
* **查询过滤**：支持在全局、实例或查询级别上应用过滤条件，以便在检索数据时自动应用这些条件。
* **查询未来**：允许将多个查询合并到单个数据库往返中，从而减少数据库往返次数，提高性能。
* **查询包含优化**：改进了 Include 方法的行为，允许在加载关联实体时应用过滤条件，从而优化生成的 SQL 语句。
* **审计跟踪**：提供审计跟踪功能，允许自动跟踪对实体的更改，并将审计信息保存到数据库中。
* **支持多个版本的 Entity Framework**：`EntityFramework-Plus` 支持 Entity Framework 5（EF5）、Entity Framework 6（EF6）和 Entity Framework Core（EF Core）。
* **易于集成**：通过 NuGet 包管理器可以轻松地将 `EntityFramework-Plus` 集成到现有的 Entity Framework 或 Entity Framework Core 项目中。


![](https://img2024.cnblogs.com/blog/1336199/202409/1336199-20240913083010792-242722612.png)


## 项目NuGet包安装


NuGet包管理器中搜索：`Z.EntityFramework.Plus.EFCore`包进行安装。


![](https://img2024.cnblogs.com/blog/1336199/202409/1336199-20240913083024481-1719178998.png)


## 批量删除


如果需要删除成百上千个实体，使用Entity Framework Core进行删除可能会非常慢。实体在被删除之前首先加载到上下文中，这对性能非常不利，然后，它们被一个接一个地删除，这使得删除操作变得更糟。



```
var ctx = new EntitiesContext();

// 删除所有2年不活动的用户
var date = DateTime.Now.AddYears(-2);
ctx.Users.Where(x => x.LastLoginDate < date)
         .Delete();

// 使用BatchSize删除
var date = DateTime.Now.AddYears(-2);
ctx.Users.Where(x => x.LastLoginDate < date)
         .Delete(x => x.BatchSize = 1000);

```

## 批量更新


如果需要更新具有相同表达式的数百或数千个实体，则使用Entity Framework Core进行更新可能会非常慢。实体在更新之前首先加载到上下文中，这对性能非常不利，然后，它们一个接一个地更新，这使得更新操作变得更糟。



```
var ctx = new EntitiesContext();

// 更新所有用户2年不活动
var date = DateTime.Now.AddYears(-2);
ctx.Users.Where(x => x.LastLoginDate < date)
         .Update(x => new User() { IsSoftDeleted = 1 });

```

## 查询过滤器


### 全局过滤器



```
// CREATE global filter
QueryFilterManager.Filter<Customer>(x => x.Where(c => c.IsActive));

var ctx = new EntityContext();

// TIP: Add this line in EntitiesContext constructor instead
QueryFilterManager.InitilizeGlobalFilter(ctx);

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.ToList();

```

### 实例过滤



```
var ctx = new EntityContext();

// CREATE filter
ctx.Filter<Customer>(x => x.Where(c => c.IsActive));

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.ToList();

```

### 查询过滤器



```
var ctx = new EntityContext();

// CREATE filter disabled
ctx.Filter<Customer>(CustomEnum.EnumValue, x => x.Where(c => c.IsActive), false);

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.Filter(CustomEnum.EnumValue).ToList();

```

## 项目源码地址


更多项目实用功能和特性欢迎前往项目开源地址查看👀，别忘了给项目一个Star支持💖。


* 开源地址：[https://github.com/zzzprojects/EntityFramework\-Plus](https://github.com)
* 在线文档：[https://entityframework\-plus.net](https://github.com)


## 优秀项目和框架精选


该项目已收录到C\#/.NET/.NET Core优秀项目和框架精选中，关注优秀项目和框架精选能让你及时了解C\#、.NET和.NET Core领域的最新动态和最佳实践，提高开发工作效率和质量。坑已挖，欢迎大家踊跃提交PR推荐或自荐（让优秀的项目和框架不被埋没🤞）。


* GitHub开源地址：[https://github.com/YSGStudyHards/DotNetGuide/blob/main/docs/DotNet/DotNetProjectPicks.md](https://github.com)
* Gitee开源地址：[https://gitee.com/ysgdaydayup/DotNetGuide/blob/main/docs/DotNet/DotNetProjectPicks.md](https://github.com)


