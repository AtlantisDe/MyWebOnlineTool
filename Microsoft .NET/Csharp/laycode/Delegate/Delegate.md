# Delegate

- [C# 委托（Delegate）](http://www.runoob.com/csharp/csharp-delegate.html)
- [EventHandler 委托的使用](https://www.cnblogs.com/hshuai/p/3585064.html)
- [关于 EventHandler 的使用](https://www.cnblogs.com/lc-ant/p/4225746.html)

## 委托

### 1. 简单委托 Demo

#### 1. 代码示例 1

```C#
// 1. 声明委托结构 2.创建委托对象 3.实例化委托 简单三步

//   step1：首先用delegate定义一个委托 。

//   step2：声明一个方法来对应委托。

//   step3：用这个方法来实例化这个委托。

//   step4：调用委托。（自己加的）

//声明没有参数,没有返回值的委托
public delegate void MyDelegate();
//委托对象
static MyDelegate myDelegate;

public static void Show()
{
    Console.WriteLine("我的代理");
}

static void Main(string[] args)
{
    myDelegate = new MyDelegate(Show);//实例化委托  委托myDelegate去做Show的事情
    myDelegate();//调用myDelegate
    Console.ReadKey();
}
```

#### 2. 代码示例 2

```C#
//Demo
public class actionitem
{
   public string  Action { get; set; }
   public bool autoexit { get; set; }

   //demo
   public delegate void RunCode();
   public RunCode myDelegate { get; set; }
}

// 匿名方法
actionitem = new DemoTestTool.Module.RunAction.Main.Entity.actionitem()
{
      Action = "",
      autoexit = true,
      autoexittimeout = 15000,
      myDelegate = new Module.RunAction.Main.Entity.actionitem.RunCode
      (
         delegate ()
         {
            System.Console.Write("Hello, ");
            System.Console.WriteLine("World!");
         }
      )
};
actionitems.Add(actionitem);

```

### 2. 声明委托（Delegate）

```C#
// 委托声明决定了可由该委托引用的方法。委托可指向一个与其具有相同标签的方法。
// 例如，假设有一个委托：
public delegate int MyDelegate (string s);

// 上面的委托可被用于引用任何一个带有一个单一的 string 参数的方法，并返回一个 int 类型变量。
// 声明委托的语法如下：
delegate <return type> <delegate-name> <parameter list>
```

### 3. 实例化委托（Delegate）

```C#
public delegate void printString(string s);
...
printString ps1 = new printString(WriteToScreen);
printString ps2 = new printString(WriteToFile);
```

### 4. 下面的实例演示了委托的声明、实例化和使用，该委托可用于引用带有一个整型参数的方法，并返回一个整型值

```C#
using System;

delegate int NumberChanger(int n);
namespace DelegateAppl
{
   class TestDelegate
   {
      static int num = 10;
      public static int AddNum(int p)
      {
         num += p;
         return num;
      }

      public static int MultNum(int q)
      {
         num *= q;
         return num;
      }
      public static int getNum()
      {
         return num;
      }

      static void Main(string[] args)
      {
         // 创建委托实例
         NumberChanger nc1 = new NumberChanger(AddNum);
         NumberChanger nc2 = new NumberChanger(MultNum);
         // 使用委托对象调用方法
         nc1(25);
         Console.WriteLine("Value of Num: {0}", getNum());
         nc2(5);
         Console.WriteLine("Value of Num: {0}", getNum());
         Console.ReadKey();
      }
   }
}
// 当上面的代码被编译和执行时，它会产生下列结果：
Value of Num: 35
Value of Num: 175

```

### 5. Demo 使用一

```C#
class Program
    {
        static void Main(string[] args)
        {
              DoTest dos = new DoTest();
              dos.DoWork += (s, e) =>
              {
                    Console.WriteLine(e.message);
              };
             dos.Begin("1");
             dos.Begin("2");
             dos.Begin("3");
             dos.Begin("4");
        }
    }
```

### 6. delegate 用法（带参数）

- [C#中 delegate 用法（带参数）](https://blog.csdn.net/zhouyingge1104/article/details/78344812)

```C#
//委托
public delegate void delegate1(string str);

//方法
private void showUpdateProgress(string content)
{
    //...
   rtbxUploadLog.Text += content;
}

//调用
delegate1 change = new delegate1(showUpdateProgress);

string resp = upload();
if (resp.Equals("ok"))
{
   this.BeginInvoke(change, "上传完成");
}else{
   this.BeginInvoke(change, "上传失败");
}
```

### 7. 匿名 委托 常用

```c#
// 那个委托返回值类型
public delegate string ChangeEveryTimesNewwordDelegate();

// 实例一个委托方法返回一个string值
StringDemoExtenions.ChangeEveryTimesNewwordDelegate newwordDelegate = new StringDemoExtenions.ChangeEveryTimesNewwordDelegate(delegate ()
{
      return RandomExtenions.Xcharacter(8);
});


NewwordDelegate newwordDelegate = new NewwordDelegate(delegate ()
{
      return RandomExtenions.Xcharacter(8);
});

// 演示方法参数中传入这个委托实例 以便提供其再下面这个方法内,灵活使用
tmp = StringDemoExtenions.ReplaceWithRegex(tmp, @"(\[随机字符\])", newwordDelegate);
```
