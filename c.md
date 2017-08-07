## C\#与C/C++的不同

* C\#数值类型不具有布尔意义。
* C\#在类型外部不能声明全局变量（也就是变量或字段）。所有字段都属于类型，而且必须在类型声明内部声明。
* C\#没有全局常量。每个常量都必须声明在类型内。
* C\#不管（函数）嵌套级别如何，都不能在第一个名字的有效范围内声明另一个同名的本地变量。
* C\#数组的方括号在基类型后，而不在变量名后。

## 类

### 字段、属性

#### 概念

字段是隶属于类的变量，可以无限制的访问公有字段。

属性是代表累的实例或类中的一个数据项成员，可以限制访问。

#### 相同

* 命名的类成员
* 有类型
* 可以被赋值和读取

#### 不同

* 属性是函数型成员，而不是数据成员
* 属性不为数据存储分配内存
* 属性执行代码

#### 属性特性

* set访问器为属性赋值
* get访问器从属性获取值

### 索引器

索引器是一组get和set访问器，与属性类似。

#### 例子

```
class Employee
{
    public string LastName;
    public string FirstName;
    public string CityOfBirth;

    public string this[int index]
    {
        set
        {
            switch(index)
            {
            case 0:
                LastName = value;
                break;
            case 1:
                FirstName = value;
                break;
            case 2:
                CityOfBirth = value;
                break;
            default:
                throw new ArgumentOutOfRangeException("index");    
            }
        }

        get
        {
            switch(index)
            {
            case 0:
                return LastName;
            case 1:
                return FirstName;
            case 2:
                return CityOfBirth;
            default:
                throw new ArgumentOutOfRangeException("index");    
            }

        }
    }
}

class Program
{
    static void Main()
    {
        Employee emp = new Employee();

        emp[0] = "Doe";
        emp[1] = "Jane";
        emp[2] = "Dallas";
        Console.WriteLine("{0}, {1}, {2}", emp[0], emp[1], emp[2]);
    }
}
```

## 数组

### Tips

* C\#不支持动态数组

* 克隆\(Clone\)值类型数组会产生两个独立数组，克隆引用类型数组会产生指向相同对象的两个数组

## 委托（delegate）

C\#中的委托相当于C++中的类型安全的、面向对象的函数指针。

```
using System;
using System.IO;

namespace HelloCSharp
{
    // boiler 类
    class Boiler
    {
        private int temp;
        private int pressure;
        public Boiler(int t, int p)
        {
            temp = t;
            pressure = p;
        }
        public int getTemp()
        {
            return temp;
        }
        public int getPressure()
        {
            return pressure;
        }
    }

    // 事件发布器
    class DelegateBoilerEvent
    {
        public delegate void BoilerLogHandler(String status);

        // 基于上面的委托定义事件
        public event BoilerLogHandler BoilerEventLog;

        public void LogProcess()
        {
            string remarks = "O. K";
            Boiler b = new Boiler(100, 12);
            int t = b.getTemp();
            int p = b.getPressure();
            if(t > 150 || t < 80 || p < 12 || p > 15) 
            {
                remarks = "Need Maintenance";
            }
            OnBoilerEventLog("Logging Info:\n");
            OnBoilerEventLog("Temparature " + t + "\nPressure: " + p);
            OnBoilerEventLog("\nMessage: " + remarks);
        }
        protected void OnBoilerEventLog(string message)
        {
            if (BoilerEventLog != null)
            {
                BoilerEventLog(message);
            }
        }
    }

    // 该类保留写入日志文件的条款
    class BoilerInfoLogger
    {
        FileStream fs;
        StreamWriter sw;
        public BoilerInfoLogger(string filename)
        {
            fs = new FileStream(filename, FileMode.Append, FileAccess.Write);
            sw = new StreamWriter(fs);
        }
        public void Logger(string info)
        {
            sw.WriteLine(info);
        }
        public void Close()
        {
            sw.Close();
            fs.Close();
        }
    }

    // 事件订阅器
    public class RecordBoilerInfo
    {
        static void Logger(string info)
        {
            Console.WriteLine(info);
        }//end of Logger

        static void Main(string[] args)
        {
            BoilerInfoLogger filelog = new BoilerInfoLogger("e:\\boiler.txt");
            DelegateBoilerEvent boilerEvent = new DelegateBoilerEvent();
            boilerEvent.BoilerEventLog += new DelegateBoilerEvent.BoilerLogHandler(Logger);
            boilerEvent.BoilerEventLog += new DelegateBoilerEvent.BoilerLogHandler(filelog.Logger);
            boilerEvent.LogProcess();
            Console.ReadLine();
            filelog.Close();
        }//end of main

    }//end of RecordBoilerInfo
}
```

## 接口

接口是指定一组函数成员，而不实现他们的引用类型。所以只能类和结构来实现接口 。

```
using System;

namespace HelloCSharp
{
    interface IInfo
    {
        string GetName();
        string GetAge();
    }

    class CA : IInfo
    {
        public string Name;
        public int Age;
        public string GetName() { return Name; }
        public string GetAge() { return Age.ToString(); }

    }

    class CB : IInfo
    {
        public string First;
        public string Last;
        public double PersonsAge;
        public string GetName() { return First + " " + Last; }
        public string GetAge() { return PersonsAge.ToString();}
    }

    class Program
    {
        static void PrintInfo(IInfo item)
        {
            Console.WriteLine("Name : {0}, Age : {1}", item.GetName(), item.GetAge());
        }

        static void Main()
        {
            CA a = new CA() { Name = "John Doe", Age = 35 };
            CB b = new CB() { First = "Jane", Last = "Doe", PersonsAge = 33 };

            PrintInfo(a);
            PrintInfo(b);
        }
    }

}
```

## 转换

转换是接受一个类型的值并使用它作为另一个类型的等价值得过程。

## 泛型

泛型特性提供了一种更优雅地方式，可以让多个类型共享一组代码。泛型允许我们声明类型参数化的代码，可以用不同的类型进行实例化。

泛型是类型的模板，类型是对象的模板。

C\#有五种泛型：类、结构、接口、委托、方法。

```
using System;

namespace HelloCSharp
{
    class MyStack<T>
    {
        T[] StackArray;
        int StackPointer = 0;

        public void Push(T x)
        {
            if (!IsStackFull)
            {
                StackArray[StackPointer++] = x;
            }
        }

        public T Pop()
        {
            return (!IsStackEmpty) ? StackArray[--StackPointer] : StackArray[0];
        }

        const int MaxStack = 10;
        bool IsStackFull { get { return StackPointer >= MaxStack;} }
        bool IsStackEmpty { get { return StackPointer <= 0;} }

        public MyStack()
        {
            StackArray = new T[MaxStack];
        }

        public void Print()
        {
            for (int i = StackPointer - 1; i >= 0; i--)
            {
                Console.WriteLine(" Value:{0}", StackArray[i]);
            }
        }
    }

    class Program
    {
        static void Main()
        {
            MyStack<int> StackInt = new MyStack<int>();
            MyStack<string> StackString = new MyStack<string>();

            StackInt.Push(3);
            StackInt.Push(5);
            StackInt.Push(7);
            StackInt.Push(9);
            StackInt.Print();

            StackString.Push("This is fun");
            StackString.Push("Hi there! ");
            StackString.Print();
        }
    }
}
```

### where

使用**where**语句**约束泛型**参数可以接受哪些类型

### 可变性（协变、逆变、不变）

协变：如果派生类只是用于输出值，那么这种结构化的委托有效性之间的常数关系叫做协变。关键字out。

逆变：在期望传入基类时，允许传入派生类对象的特性叫做逆变。

```
delegate T Factory<out R, in S, T>();
```

## 枚举器和迭代器

### 枚举器

枚举器可以依次返回请求的数组中的元素

#### IEnumerator接口

* GetEnumerator\(\)：获取枚举器
* Current：返回当前位置的项
* MoveNext\(\)：前进位置到下一项
* Reset\(\)：把位置设置回原始配置

#### 使用IEnumerable和IEnumerator的示例（非泛型）

```
using System;
using System.Collections;

namespace HelloCSharp
{
    class ColorEnumerator : IEnumerator
    {
        string[] _colors;
        int _position = -1;

        public ColorEnumerator(string[] theColors)
        {
            _colors = new string[theColors.Length];
            for (int i = 0; i < theColors.Length; i++)
            {
                _colors[i] = theColors[i];
            }
        }

        public object Current
        {
            get
            {
                if (_position == -1 || _position >= _colors.Length)
                    throw new InvalidOperationException();

                return _colors[_position];
            }
        }

        public bool MoveNext()
        {
            if (_position < _colors.Length - 1)
            {
                _position++;
                return true;
            }
            else
            {
                return false;
            }
        }

        public void Reset()
        {
            _position = -1;
        }
    }

    class Spectrum : IEnumerable
    {
        string[] Colors = { "violet", "blue", "cyan", "green", "yellow", "orange", "red" };

        public IEnumerator GetEnumerator()
        {
            return new ColorEnumerator(Colors);
        }
    }

    class Program
    {
        static void Main()
        {
            Spectrum spectrum = new Spectrum();
            foreach (string color in spectrum)
                Console.WriteLine(color);
        }
    }
}
```

### 迭代器

可以通过创建迭代器来返回**可枚举类型\(**IEnumerable\)或枚举器\(IEnumerator\)

需要`using System.Collections.Generic`

#### 枚举器的迭代器模式

```
class MyClass
{
    public IEnumerator<string> GetEnumerator()
    {
        return IteratorMethod();
    }

    public IEnumerator<string> IteratorMethod()
    {
        ...
        yield return ...;
        yield return ...;
    }
}

Main
{
    MyClass mc = new MyClass();

    foreach(string x in mc)
        ...
}
```

#### 可枚举类型的迭代器模式

```
class MyClass
{
    public IEnumerator<string> GetEnumerator()
    {
        return IteratorMethod().GetEnumerator();
    }

    public IEnumerable<string> IteratorMethod()
    {
        ...
        yield return ...;
        yield return ...;
    }
}

Main
{
    MyClass mc = new MyClass();

    foreach(string x in mc)
        ...

    foreach(string x in mc.IteratorMethod())
        ...   
}
```

> [使用迭代器（C\# 编程指南）](https://msdn.microsoft.com/zh-cn/library/65zzykke%28v=vs.100%29.aspx)

## LINQ

LINQ（发音为link）代表语言集成查询（Language Integrated Query），是.NET 框架的扩展，允许我们使用SQL查询数据库的方式来查询数据集合（数据库、程序对象的集合、XML文档）

```
class LINQQueryExpressions
{
    static void Main()
    {

        // Specify the data source.
        int[] scores = new int[] { 97, 92, 81, 60 };

        // Define the query expression.
        IEnumerable<int> scoreQuery =
            from score in scores
            where score > 80
            select score;

        // Execute the query.
        foreach (int i in scoreQuery)
        {
            Console.Write(i + " ");
        }            
    }
}

// Output: 97 92 81
```

### 扩展：匿名类型\(anonymous type\)

匿名类型对象初始化可以有三种形式：赋值形式、简单标识符、成员访问表达式。后两种形式叫做**投影初始化语句（projection initializer）。**

```
class Other
{
    static public string Name = "Mary Jones";
}

class Program
{
    static Void Main()
    {
        string Major = "History";

        var student = new {Age = 19, Other.Name, Major};

        Console.WriteLine("{0}, Age {1}, Major: {2}", student.Name, student,Age, student.Major);
    }    
}

// Output: Mary Jones, Age 19, Major: History
```

### from子句

```
int[] arr = {10, 11, 12};

var query = from item in arr
            where item < 11
            select item;

foreach(var item in query)
    Console.Write("{0}", item);
```

### where子句

where子句根据之后的运算来除去不符合指定条件的项

### select...group子句

* select 子句
* group...by 子句

指定数据源和要选择的对象

### orderby子句

```
var query = from student in students
            orderby student.Age (ascending(升序)/descending(降序))
            select student;
```

### join\(联结\)子句

两张表联结起来：LastName -&gt; StID -&gt; CourseName

```
class Program
{
    public class Student
    {
        public int StID;
        public string LastName;
    }

    public class CourseStudent
    {
        public string CourseName;
        public int StID;
    }

    static Student[] students = new Student[]
    {
        new Student{StID = 1; LastName = "Carson"},
        new Student{StID = 2; LastName = "Klassen"},
        new Student{StID = 3; LastName = "Fleming"},
    };

    static CourseStudent[] studentInCourses = new CourseStudent[]
    {
        new CourseStudent{CourseName = "Art", StID = 1},
        new CourseStudent{CourseName = "Art", StID = 2},
        new CourseStudent{CourseName = "History", StID = 1},
        new CourseStudent{CourseName = "History", StID = 3},
        new CourseStudent{CourseName = "Physics", StID = 3},
    };

    static void Main()
    {
        // 查询所有选择了历史课的学生的姓氏
        var query = from s in students
                join c in studentsInCourses on s.StID equals c.StID
                 where c.CourseName == "History"
                select s.LastName;

        // 显示所有选择了历史课的学生的姓氏
        foreach (var q in query)
            Console.WriteLine("Student taking History: {0}", q);
    }
}
```

### let子句

let子句接受一个表达式的运算并把它赋值给一个需要在其他运算中使用的标识符。

```
var someInts = from a in groupA
               form b in groupB
               let sum = a + b
               where sum == 12
               select new {a, b, sum};
```

### group子句

group子句ba2select的对象根据一些标准进行分组

```
var someInts = from student in students
               group student by student.Majorl;
```

### into子句（查询延续）

查询延续子句可以接受查询的一部分结果并赋予一个名字，从而可以在查询的另一部分中使用。

```
var someInts = from a in groupA
               join b in groupB on a equals b
               into groupAandB
               from c in groupAandB
               select c;
```

> [LINQ 标准查询操作概述 ](http://www.cnblogs.com/liqingwen/p/5801249.html)

### ![](http://images2015.cnblogs.com/blog/711762/201608/711762-20160825102717839-1252282113.png)LINQ to XML

#### XML

```
using System;
using System.Xml.Linq;            // 需要的命名空间

class Program
{
    static void Main()
    {
        XDocument employees1 = 
            new XDocument(                                // 创建XML文档
                new XElement("Employees",                 // 创建根元素    
                    new XElement("Name", "Bob Smith"),    // 创建元素
                    new XElement("Name", "Bob Smith")     // 创建元素
                )
            );

        // 保存到文件
        employees1.Save("EmployeesFile.xml");

        // 将保存的文档加载到新变量中    
        XDocument employees2 = new XDocument.Load("EmployeesFile.xml");

        // 显示文档
        Console.WriteLine(employees2);
    }
}
```



