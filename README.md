---
seo_title: High performance, high productivity, ultra lightweight ORM
keywords: SmartSql, MyBatis ,Cache(Memory | Redis) ,ZooKeeper , R/W Splitting , Dynamic Repository,ORM,DotNet,.Net,dotnet core
description :  High performance, high productivity, ultra lightweight ORM,SmartSql = MyBatis + Cache(Memory | Redis) + ZooKeeper + R/W Splitting +Dynamic Repository
---

<p align="center">
  <a href="https://github.com/Ahoo-Wang/SmartSql" target="_blank"><img width="100"src="./imgs/SmartSql.png"></a>
</p>

# Introduction

## Why

- Embracing Cross-platform DotNet Core, it's time.
- High performance, high productivity, ultra lightweight ORM. **156kb** (Dapper:**168kb**)

## So SmartSql

- TargetFrameworks: .NETFramework 4.6 & .NETStandard 2.0
- SmartSql = SmartSql = MyBatis + Cache(Memory | Redis) + ZooKeeper + R/W Splitting +Dynamic Repository + ......

## Main feature

- 1 ORM
  - 1.1 Sync
  - 1.2 Async
- 2 XmlConfig & XmlStatement -> Sql
  - 2.1 SmartSqlMapConfig & SmartSqlMap (Yes, you guessed it, like MyBatis, separating SQL via XML configuration.)
  - 2.2 Config Hot Update ->ConfigWatcher & Reload (Configuration file hot update: When you need to modify the Sql, directly modify the SqlMap configuration file, save it.)
- 3 Read and write separation
  - 3.1 Read and write separation
  - 3.2 Multi-read library weight filtering (configure multi-read library, select read library according to read library weight)
- 4 Logging
  - 4.1 Based on Microsoft.Extensions.Logging.Abstractions (when you need to track debugging, everything is so clear at a glance)
- 5 Dynamic Repository
  - 5.1 SmartSql.DyRepository  (Free your hands, you define the storage interface, I will implement database access)
- 6 Query cache (hot data cache, a configuration is easy to get)
  - 6.1 SmartSql.Cache.Memory
    - 6.1.1 Fifo
    - 6.1.2 Lru
  - 6.2 SmartSql.Cache.Redis
  - 6.3 Cache transaction consistency
- 7 Distributed configuration plugin
  - 7.1 IConfigLoader (profile loader)
  - 7.2 LocalFileConfigLoader  (local file configuration loader)
    - 7.2.1 Load SmartSqlMapSource Xml
    - 7.3.1 Load SmartSqlMapSource Directory
  - 7.3 SmartSql.ZooKeeperConfig (ZooKeeper Distributed Profile Loader)

## Performance evaluation

``` ini

BenchmarkDotNet=v0.10.14, OS=Windows 10.0.17134
Intel Core i7-6700K CPU 4.00GHz (Skylake), 1 CPU, 8 logical and 4 physical cores
.NET Core SDK=2.1.201
  [Host]     : .NET Core 2.0.7 (CoreCLR 4.6.26328.01, CoreFX 4.6.26403.03), 64bit RyuJIT
  DefaultJob : .NET Core 2.0.7 (CoreCLR 4.6.26328.01, CoreFX 4.6.26403.03), 64bit RyuJIT
```

|            ORM |                     Type |                  Method |        Return |      Mean |     Error |    StdDev | Rank |     Gen 0 |     Gen 1 |     Gen 2 | Allocated |
|--------------- |------------------------- |------------------------ |-------------- |----------:|----------:|----------:|-----:|----------:|----------:|----------:|----------:|
|         Native |         NativeBenchmarks |   Query_GetValue_DbNull | IEnumerable`1 |  78.39 ms | 0.8935 ms | 0.7921 ms |    1 | 3000.0000 | 1125.0000 |  500.0000 |  15.97 MB |
|       SmartSql |       SmartSqlBenchmarks |                   Query | IEnumerable`1 |  78.46 ms | 0.2402 ms | 0.1875 ms |    1 | 2312.5000 | 1000.0000 |  312.5000 |  12.92 MB |
| SmartSqlDapper | SmartSqlDapperBenchmarks |                   Query | IEnumerable`1 |  78.65 ms | 1.2094 ms | 1.1312 ms |    1 | 3687.5000 | 1437.5000 |  687.5000 |  19.03 MB |
|         Native |         NativeBenchmarks | Query_IsDBNull_GetValue | IEnumerable`1 |  78.84 ms | 0.8984 ms | 0.7502 ms |    1 | 2312.5000 | 1000.0000 |  312.5000 |  12.92 MB |
|         Dapper |         DapperBenchmarks |                   Query | IEnumerable`1 |  79.00 ms | 1.0949 ms | 0.9706 ms |    1 | 3312.5000 | 1312.5000 |  625.0000 |  17.19 MB |
|             EF |             EFBenchmarks |                   Query | IEnumerable`1 |  79.44 ms | 1.6880 ms | 1.5789 ms |    1 | 6250.0000 |         - |         - |  26.05 MB |
|       SqlSugar |       SqlSugarBenchmarks |                   Query | IEnumerable`1 |  81.09 ms | 0.8718 ms | 0.7728 ms |    2 | 2187.5000 |  875.0000 |  250.0000 |  12.64 MB |
|          Chloe |          ChloeBenchmarks |                   Query | IEnumerable`1 |  83.86 ms | 1.2714 ms | 1.1893 ms |    3 | 2250.0000 |  937.5000 |  312.5000 |  12.62 MB |
|             EF |             EFBenchmarks |                SqlQuery | IEnumerable`1 |  89.11 ms | 0.7562 ms | 0.6314 ms |    4 | 8187.5000 |  125.0000 |         - |  33.68 MB |
|             EF |             EFBenchmarks |        Query_NoTracking | IEnumerable`1 |  93.13 ms | 0.8458 ms | 0.7912 ms |    5 | 5875.0000 | 2250.0000 | 1062.5000 |  29.71 MB |
|             EF |             EFBenchmarks |     SqlQuery_NoTracking | IEnumerable`1 | 106.89 ms | 1.0998 ms | 1.0288 ms |    6 | 7437.5000 | 2875.0000 | 1312.5000 |  37.34 MB |

---

## Nuget Packages

| Package | NuGet Stable |  Downloads |
| ------- | -------- | ------- |
| [SmartSql](https://www.nuget.org/packages/SmartSql/) | [![SmartSql](https://img.shields.io/nuget/v/SmartSql.svg)](https://www.nuget.org/packages/SmartSql/)  | [![SmartSql](https://img.shields.io/nuget/dt/SmartSql.svg)](https://www.nuget.org/packages/SmartSql/) |
| [SmartSql.TypeHandler](https://www.nuget.org/packages/SmartSql.TypeHandler/) | [![SmartSql.TypeHandler](https://img.shields.io/nuget/v/SmartSql.TypeHandler.svg)](https://www.nuget.org/packages/SmartSql.TypeHandler/)  | [![SmartSql.TypeHandler](https://img.shields.io/nuget/dt/SmartSql.TypeHandler.svg)](https://www.nuget.org/packages/SmartSql.TypeHandler/) |
| [SmartSql.DyRepository](https://www.nuget.org/packages/SmartSql.DyRepository/) | [![SmartSql.DyRepository](https://img.shields.io/nuget/v/SmartSql.DyRepository.svg)](https://www.nuget.org/packages/SmartSql.DyRepository/)  | [![SmartSql.DyRepository](https://img.shields.io/nuget/dt/SmartSql.DyRepository.svg)](https://www.nuget.org/packages/SmartSql.DyRepository/) |
| [SmartSql.DIExtension](https://www.nuget.org/packages/SmartSql.DIExtension/) | [![SmartSql.DIExtension](https://img.shields.io/nuget/v/SmartSql.DIExtension.svg)](https://www.nuget.org/packages/SmartSql.DIExtension/)  | [![SmartSql.DIExtension](https://img.shields.io/nuget/dt/SmartSql.DIExtension.svg)](https://www.nuget.org/packages/SmartSql.DIExtension/) |
| [SmartSql.Cache.Redis](https://www.nuget.org/packages/SmartSql.Cache.Redis/) | [![SmartSql.Cache.Redis](https://img.shields.io/nuget/v/SmartSql.Cache.Redis.svg)](https://www.nuget.org/packages/SmartSql.Cache.Redis/)  | [![SmartSql.Cache.Redis](https://img.shields.io/nuget/dt/SmartSql.Cache.Redis.svg)](https://www.nuget.org/packages/SmartSql.Cache.Redis/) |
| [SmartSql.ZooKeeperConfig](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/) | [![SmartSql.ZooKeeperConfig](https://img.shields.io/nuget/v/SmartSql.ZooKeeperConfig.svg)](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/)  | [![SmartSql.ZooKeeperConfig](https://img.shields.io/nuget/dt/SmartSql.ZooKeeperConfig.svg)](https://www.nuget.org/packages/SmartSql.ZooKeeperConfig/) |
| [SmartSql.Options](https://www.nuget.org/packages/SmartSql.Options/) | [![SmartSql.Options](https://img.shields.io/nuget/v/SmartSql.Options.svg)](https://www.nuget.org/packages/SmartSql.Options/)  | [![SmartSql.Options](https://img.shields.io/nuget/dt/SmartSql.ZooKeeperConfig.svg)](https://www.nuget.org/packages/SmartSql.Options/) |

## Demo

>[SmartSql-Starter](https://github.com/Ahoo-Wang/SmartSql-Starter)

## Document

- [Online reading address](https://doc-en.smartsql.net/)

## Document contributor

- [Ahoo-Wang](https://github.com/Ahoo-Wang)
- [RocherKong](https://github.com/RocherKong)
- [ElderJames](https://github.com/ElderJames)