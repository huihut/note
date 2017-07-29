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



