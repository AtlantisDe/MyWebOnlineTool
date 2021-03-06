# Interlocked.Increment Method

- 原子操作
- [Interlocked.Increment Method (System.Threading)](https://docs.microsoft.com/en-us/dotnet/api/system.threading.interlocked.increment?view=netframework-4.8)
- [C#如何在多线程中同步读写一个共有属性？请大神们赐教！！！*已解决*博问\_博客园](https://q.cnblogs.com/q/89954/)

## 常用

### 1. 常用代码

```c#
System.Threading.Interlocked.Increment(ref visits);
System.Threading.Interlocked.Add(ref visits,2);
```

### 2. 常用 DEMO

```c#
public static bool Go()
{
    long visits = 0;
    Parallel.For(0, 10000000, new ParallelOptions() { MaxDegreeOfParallelism = 5000 }, (i, loopState) =>
    {
        System.Threading.Interlocked.Increment(ref visits);
    });
    return true;
}
```

### 3. 非局部变量原子操作

```c#
var ht = new System.Collections.Hashtable
{
    { "aa", AnalysisItem }
};

Parallel.For(0, 10000000, new ParallelOptions() { MaxDegreeOfParallelism = 5000 }, (i, loopState) =>
{
    lock (ht.SyncRoot)
    {
        var aaa = (AnalysisItem)ht["aa"];
        aaa.RequestTotalTimes += 1;
    }
});

```
