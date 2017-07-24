\#\#\# 常成员函数



\*\*声明：&lt;类型标志符&gt;函数名（参数表）const；\*\*



    class A

    {

    private:

        const int a;    //常对象成员

        

    public:

        int getValue\(\) const;   //常成员函数

        int getValue\(\);     //普通成员函数

    };



    int main\(\)

    {

        const A a\(\);        //常对象

        canst A \*p = &a;    //常指针

        canst A &q = a;     //常引用

    }   





\*\*说明\*\*：



1. \*\*常对象只能调用常成员函数\*\*，不能更新类的成员变量，也不能调用该类中没有用const修饰的成员函数。

2. \*\*普通对象可以调用全部成员函数\*\*。

3. const关键字可以用于对\*\*重载函数\*\*的区分。

3. 当对一个对象调用成员函数时，编译程序先将对象的地址赋给this指针，然后调用成员函数，每次成员函数存取数据成员时，由\*\*隐含使用this指针\*\*。

4. 当一个成员函数被调用时，自动向它传递一个隐含的参数，该参数是一个指向这个成员函数所在的对象的指针。 

5. 在C++中，this指针被隐含地声明为: X \* const this,这意味着 \*\*不能给this 指针赋值\*\*。

6. 由于this并不是一个常规变量，所以，\*\*不能取得this的地址\*\*。



&lt;!-- more --&gt;



    

\#\# 函数



\#\#\# 函数默认值



赋值前面定义的变量之前必须要先赋值后面定义的变量



    void fun\(int a, int b, int c\);  //没有赋值

    

    void fun\(int a, int b, int c = 30\); //可以 

    void fun\(int a, int b = 20, int c = 30\);    //可以

    void fun\(int a = 10, int b = 20, int c = 30\);  //可以

    

    void fun\(int a = 10, int b, int c\);    //不可以

    void fun\(int a = 10, int b, int c = 30\);    //不可以

    

一般函数声明赋默认值，函数定义不赋值



    void fun\(int a = 10, int b = 20, int c = 30\);  //声明

    void fun\(int a, int b, int c\)

    {

        std::cout &lt;&lt; a+b+c &lt;&lt; std::endl;

    }   

    

函数实现时赋值，只覆盖前面的值



    void fun\(int a = 10, int b = 20, int c = 30\);  //声明

    

    int main\(\)

    {

        fun\(\);              //a=10 b=20 c=30 

        fun\(100\);           //a=100 b=20 c=30

        fun\(100,200\);       //a=100 b=200 c=30

        fun\(100,200,300\);   //a=100 b=200 c=300

        return 0;

    }

    

    void fun\(int a, int b, int c\)

    {

        std::cout &lt;&lt; a+b+c &lt;&lt; std::endl;

    }

    

\#\#\# 构造函数和析构函数

构造函数和析构函数没有返回值，有返回值是成员函数。



\* 复制构造函数





    class Point

    {

    public:

        Point\(int xx,int yy\){X=xx;Y=yy;}

        Point\(const Point& p\);

        int getX\(\){returnX;}

        int getY\(\){returnY;}

    private:

        intX,Y;

    };

    Point::Point\(const Point& p\)

    {

        X=p.X;

        Y=p.Y;

        std::cout&lt;&lt;"拷贝构造函数调用"&lt;&lt;std::endl;

    }

    int main\(\)

    {

        Point p1\(1,2\);

        Point p2\(p1\);

        return 0;

    }

    

\#\#\# 内联函数

内联函数



\* 相当于把内联函数里面的内容写在调用内联函数处；



\* 相当于不用执行进入函数的步骤，直接执行函数体；



\* 相当于宏，却比宏多了类型检查，真正具有函数特性。





内联函数不能包含循环、递归、switch等复杂操作。

    

    inline void fun\(int a\)

    {

        std::cout&lt;&lt; a &lt;&lt;std::endl;

    }

    int main\(\)

    {

        int x = 1;

        fun\(x\);     //相当于执行std::cout&lt;&lt; x &lt;&lt;std::endl;

        return 0;

    }

    

    

\#\# 引用

\* 引用必须初始化，初始化后无法再去引用另一个对象



\* 引用后具有该数据类型的所有操作



    

    int main\(\)

    {

        int a = 1;

        int &b = a;

        b++;

        std::cout&lt;&lt; "a=" &lt;&lt; a &lt;&lt; ", b=" &lt;&lt; b &lt;&lt;endl;   //a=2, b=2

        return 0;

    }

    

\#\# 内存管理

\#\#\# new\(申请\) / delete（释放）



\* 使用 new 申请内存，使用 delete 释放内存

\* 申请内存需要判断是否成功，释放内存需要设空指针

\* new 与 delete 配套使用





    int main\(\)

    {

        int \*p = new int;       //申请内存

        int \*arr = new int\[10\]; //申请块内存

        

        //赋值、输出

        \*p = 2;

        std::cout &lt;&lt; \*p &lt;&lt;std::endl;

        

        for\(int i = 0; i &lt; 10; i++\)

        {

            arr\[i\] = i;

            std::cout &lt;&lt; arr\[i\] &lt;&lt;std::endl;

        }

        

        //释放内存

        delete p;   //释放p

        p = NULL;   //置空p

        

        delete \[\]arr;   //释放arr

        arr = NULL;     //置空arr

        

        //申请大内存

        int \*q = new int\[10000\]; 

        

        if\(NULL == q\)

        {

            std::cout &lt;&lt; "内存分配失败" &lt;&lt;std::endl;

        }

        else

        {

            std::cout &lt;&lt; "内存分配成功" &lt;&lt;std::endl;

        }

        

        delete \[\]q;     //释放

        q = NULL;       //置空

    }



\#\# 类



\#\#\# 抽象类



含有纯虚函数的类叫做抽象类。  



只有实现了抽象类全部纯虚函数的子类才可以创建对象。



\#\#\# 接口类



仅含有纯虚函数的抽象类叫做接口类。







\#\#\# 聚合类

用户可以直接访问其成员，并且具有特殊的初始化语法形式。



满足如下特点：

	

\* 所有成员都是public

\* 没有有定于任何构造函数

\* 没有类内初始化

\* 没有基类，也没有virtual函数



如下：



	//定义：

	struct Date 

	{

		int ival;

		string s;

	}



	//初始化：

	Data vall = { 0, "Anna" };

	

	

\#\#\# 字面值常量类

数据成员都是字面值类型的聚合类是字面值常量类







\#\#\# 访问限定符



\* public ： 公共的

\* protected ： 受保护的

\* private   :   私有的



\#\# 对象



\#\#\# 对象的实例化



\* 从栈中实例化  





    A a;

    A a\[10\];



\* 从堆中实例化





    A \*p = new A\(\);     //Tips：与 A \*p = new A; 一样 

    A \*q = new A\[10\];

    



\* \*\*Tips：对象指针 = new 类名（&lt;初始值列表&gt;）;\*\*  

当A的构造函数没有参数可以省略括号；  

当A的构造函数有参数是不能省略括号，而且要填写传入参数。





\#\#\# 对象的拷贝



\* 浅拷贝——只是对象数据的拷贝（指针类型拷贝到的是地址）

\* 深拷贝——对对象本身进行重新构建（指针类型重新开辟内存进行拷贝数据）



\#\#\# new 与 malloc 的不同



\* new 会调用对象的构造函数，malloc不会，仅仅分配内存。



\#\# 初始化列表



&gt; http://www.cnblogs.com/graphics/archive/2010/07/04/1770900.html



\* 初始化类的成员有两种方式，一是\*\*使用初始化列表\*\*，二是\*\*在构造函数体内\*\*进行赋值操作。



\* \*\*初始化列表\*\*是构造函数进行初始化的一种方式，在构造函数后面以冒号开头，后跟一系列以逗号分隔的初始化字段。





    class Animal

    {

    public:

        Animal\(int weight,int height\):     //A初始化列表

        m\_weight\(weight\),

        m\_height\(height\)

        {

        }

        Animal\(int weight,int height\)     //B函数体内初始化

        {

            m\_weight = weight;

            m\_height = height;

        }

    private:

        int m\_weight;

        int m\_height;

    }





\*\*tips：A与B不能同时存在\*\*



\#\#\# 使用初始化列表的好处：



\* 更高效：少了一次调用默认构造函数的过程。



\* 有些场合必须要用初始化列表：

&gt; 1. 常量成员，因为常量只能初始化不能赋值，所以必须放在初始化列表里面

&gt;2. 引用类型，引用必须在定义的时候初始化，并且不能重新赋值，所以也要写在初始化列表里面

&gt;3. 没有默认构造函数的类类型，因为使用初始化列表可以不必调用默认构造函数来初始化，而是直接调用拷贝构造函数初始化。





\#\# operator操作符



\#\#\# 含义



operator是操作符的意思。它和运算符一起使用，表示一个运算符函数，理解时应将operator=整体上视为一个函数名。



\* 运算符重载的本质是函数的重载



\#\#\# 一元运算符重载



\#\#\#\#\#  1.（负号）- 的重载





\* 友元函数重载

  



    class Coordinate

    {

    friend Coordinate& operator-\(Coordinate &coor\); //友元函数

    public:

        Coordinate\(int x, int y\);

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate& Coordinate::operator-\(Coordinate &coor\)

    {

        coor.m\_ix = -coorm\_ix；

        coor.m\_iy = -coor.m\_iy；

        return \*this;

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        -coor1;     //相当于operator-\(coor1\);

        return 0;

    }

    

\* 成员函数重载





    class Coordinate

    {

    public:

        Coordinate\(int x, int y\);

        Coordinate& operator-\(\);    //成员函数

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate& Coordinate::operator-\(\)

    {

        m\_ix = -m\_ix；

        m\_iy = -m\_iy；

        return \*this;

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        -coor1;     //相当于coor1.operator-\(\);

        return 0;

    }

    

    

\#\#\#\#\# 2. \(自增\) ++ 的重载



\* 前置 ++ 符号重载（成员函数重载）





    class Coordinate

    {

    public:

        Coordinate\(int x, int y\);

        Coordinate& operator++\(\);    //前置++

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate& Coordinate::operator++\(\)

    {

        m\_ix++；

        m\_iy++；

        return \*this;

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        ++coor1;     //相当于coor1.operator++\(\);

        return 0;

    }





\* 后置 ++ 符号重载（成员函数重载）





    class Coordinate

    {

    public:

        Coordinate\(int x, int y\);

        Coordinate& operator++\(int\);    //后置++

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate& Coordinate::operator++\(int\)

    {

        Coordinate old\(\*this\);

        m\_ix++；

        m\_iy++；

        return old;

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        coor1++;     //相当于coor1.operator++\(0\);

        return 0;

    }



\#\#\# 二元运算符重载



\#\#\#\#\#  1.（负号）- 的重载





\* 友元函数重载

 



    class Coordinate

    {

    friend Coordinate operator+\(const Coordinate &c1, const Coordinate &c2\);    // 重载+

    public:

        Coordinate\(int x, int y\);

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate operator+\(const Coordinate &c1, const Coordinate &c2\)

    {

        Coordinate temp;

        temp.m\_ix = c1.m\_ix + c2.m\_ix；

        temp.m\_iy = c1.m\_iy + c2.m\_iy；

        return temp;    

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        Coordinate coor2\(5,6\);

        Coordinate coor3\(0,0\);

        coor3 = coor1 + coor2;  //相当于operator+\(coor1, coor2\); 

        return 0;

    }

    



\*  成员函数重载

    



    class Coordinate

    {

    public:

        Coordinate\(int x, int y\);

        Coordinate operator+\(const Coordinate &coor\);    // 重载+

    private:

        int m\_ix;

        int m\_iy;

    }

    Coordinate& Coordinate::operator++\(const Coordinate &coor\)

    {

        Coordinate temp;

        temp.m\_ix = this-&gt;m\_ix + coor.m\_ix；

        temp.m\_iy = this-&gt;m\_iy + coor.m\_iy；

        return temp;    

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        Coordinate coor2\(5,6\);

        Coordinate coor3\(0,0\);

        coor3 = coor1 + coor2;  //相当于coor1.operator+\(coor2\); 

        return 0;

    }

    

\#\#\#\#\#  1.（输出）&lt;&lt; 的重载 \(用友元函数重载，\*\*&lt;&lt; 不可以用成员函数重载\*\*\)





    class Coordinate

    {

    friend ostream& operator&lt;&lt;\(ostream &out, const Coordinate &coor\);    // 重载&lt;&lt;

    public:

        Coordinate\(int x, int y\);

    private:

        int m\_ix;

        int m\_iy;

    }

    ostream& operator&lt;&lt;\(ostream &out, const Coordinate &coor\)

    {

        out &lt;&lt; coor.m\_ix &lt;&lt; "," &lt;&lt;  coor.m\_iy；

        return out;    

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        cout &lt;&lt; coor;   //相当于operator&lt;&lt;\(cout, coor\); 

        return 0;

    }



\#\#\#\#\#  1.（索引运算符）\[\] 的重载 \(用成员函数重载，\[\]不能用友元函数重载\)





    class Coordinate

    {

    public:

        Coordinate\(int x, int y\);

        int opetator \[\]\(int index\);

    private:

        int m\_ix;

        int m\_iy;

    }

    int Coordinate::operator \[\]\(int index\)

    {

        if\(0 == index\) return m\_ix;

        if\(1 == index\) return m\_iy;

    }

    int main\(\)

    {

        Coordinate coor1\(3,4\);

        cout &lt;&lt; coor\[0\];    //相当于coor.operator\[\]\(0\);

        cout &lt;&lt; coor\[1\];    //相当于coor.operator\[\]\(1\);

        return 0;

    }





\#\#\# 功能用法

\#\#\#\# 1. 操作符重载（operator overloading）



&gt; 格式如下：类型T operator 操作符 \(\)



    template&lt;typename T&gt; class A

    {

    public:

        const T operator + \(const T& rhs\)    //重载 + 号运算符

        {

        return this-&gt;m\_ + rhs;

        }

    private:

        T m\_;

    };



\#\#\#\# 2. 操作隐式转换（operator casting）



&gt; 格式如下： operator 类型T \(\)



    class A

    {

    public:

        operator   B\* \(\) { return this-&gt;b\_;}

        operator const   B\* \(\) {return this-&gt;b\_;}

        operator   B& \(\) {return \*this-&gt;b\_;}

    private:

        B\* b\_;

    };

    

    A a;

    //当if\(a\)，编译时，其中它转换成if\(a.operator B\*\(\)\)，其实也就是判断 if\(a.b\_\)



\#\# 面向对象特征——封装、继承、多态



!\[面向对象特征\]\(http://img.my.csdn.net/uploads/201211/22/1353564524\_6375.png\)



\#\# 封装



\* 把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。

\* 关键字：public, protected, friendly, private。不写默认为 friendly。





关键字    \| 当前类 \| 包内 \| 子孙类 \| 包外 

----------\|--------\|------\|--------\|------

public    \|   √    \|   √  \|   √    \|  √ 

protected \|   √    \|   √  \|   √    \|  × 

friendly  \|   √    \|   √  \|   ×    \|  × 

private   \|   √    \|   ×  \|   ×    \|  × 





    class A

    {

    public:

        ...

    protected:

        ...

    private:

    ...

    }



\#\# 继承



\* 基类（子类）——&gt; 派生类（父类）





\#\# 多态



\* 多态，即多种状态，在面向对象语言中，接口的多种不同的实现方式即为多态。多态性在C++中是通过虚函数来实现的。

\* 多态是以封装和继承为基础的。



\#\#\# 静态多态（早绑定）



    class A

    {

    public:

        void do\(int a\);

        void do\(int a, int b\);

    }



\#\#\# 动态多态（晚绑定）



\* 用 virtual 修饰成员函数，使其成为虚函数



\*\*注意：\*\*

\* 普通函数不能是虚函数

\* 静态函数不能是虚函数

\* 内联函数不能是虚函数

\* 构造函数不能是虚函数  





    class Shape     //形状类

    {

    public:

        virtual double calcArea\(\)

        {

            ...

        }

        

    }

    class Circle : public Shape     //圆形类

    {

    public:

        virtual double calcArea\(\);

        ...

    }

    class Rect : public Shape       //矩形类

    {

    public:

        virtual double calcArea\(\);

        ...

    }

    int main\(\)

    {

        Shape \* shape1 = new Circle\(4.0\);

        Shape \* shape2 = new Rect\(5.0, 6.0\);

        shape1-&gt;calcArea\(\);     //调用圆形类里面的方法

        shape2-&gt;calcArea\(\);     //调用矩形类里面的方法

        return 0；

    }

    

\* 虚析构函数





    class Shape

    {

    public:

        Shape\(\);        //构造函数不能是虚函数

        virtual double calcArea\(\);

        virtual ~Shape\(\);    //虚析构函数

    }

    class Circle : public Shape     //圆形类

    {

    public:

        virtual double calcArea\(\);

        ...

    }

    int main\(\)

    {

        Shape \* shape1 = new Circle\(4.0\);

        shape1-&gt;calcArea\(\);    

        delete shape1;      //因为是虚析构函数，所以调用子类析构函数后，也调用父类析构函数。

        shape1 = NULL;

        return 0；

    }





\* 纯虚函数 （含有纯虚函数的类叫做抽象类）

    

    

    virtual int A\(\) = 0; 





\#\# 运行时类型识别（RTTI）





    class Flyable                       //【能飞的】

    {

    public:

        virtual void takeoff\(\) = 0;    //起飞

        virtual void land\(\) = 0;       //降落

    }

    class Bird : public Flyable         //【鸟】

    {

    public:

        void foraging\(\) {...}           //觅食

        virtual void takeoff\(\) {...}

        virtual void land\(\) {...}

    }

    class Plane : public Flyable        //【飞机】

    {

    public:

        void carry\(\) {...}              //运输

        virtual void take off\(\) {...}

        virtual void land\(\) {...}

    }

    

    class type\_info

    {

    public:

        const char\* name\(\) const;

        bool operator == \(const type\_info & rhs\) const;

        bool operator != \(const type\_info & rhs\) const;

        int before\(const type\_info & rhs\) const;

        virtual ~type\_info\(\);

    private:

        ...

    }

    

    class doSomething\(Flyable \*obj\)     //【做些事情】

    {

        obj-&gt;takeoff\(\);



        cout &lt;&lt; typeid\(\*obj\).name\(\) &lt;&lt; endl;    //输出传入对象类型（Bird or Plane）

        

        if\(typeid\(\*obj\) == typeid\(Bird\)\)    //判断对象类型

        {

            Bird \*bird = dynamic\_cast&lt;Bird \*&gt;\(obj\); //对象转化

            bird-&gt;foraging\(\);

        }



        obj-&gt;land\(\);

    }

    

    

\* dynamic\_cast 注意事项：

1. 只能应用于指针和引用的转化

2. 要转化的类型中必须包含虚函数

3. 转化成功返回子类的地址，转化失败返回NULL



\* typeid 注意事项：

1. type\_id 返回一个 type\_info 对象的引用

2. 如果想通过基类的指针获得派生类的数据类型，基类必须带有虚函数

3. 只能获取对象的实际类型



\#\# 异常处理



    try{

        ...

    }catch\(Exception e\){

        ...

    }

    

    throw ...

    

    

\#\# 友元类和友元函数



\* 能访问私有成员  

\* 破坏封装性

\* 友元关系不可传递

\* 友元关系的单向性

\* 友元声明的形式及数量不受限制



\#\# 预处理



\*\*预处理器：\*\*

    

预处理器是为了确保头文件多次包含仍能安全工作的常用的技术。



\*\*头文件保护符：\*\*



    \#define     //把一个名字设定为预处理变量

    

    //检查某个指定的预处理变量是否已经定义

    \#ifdef      //当且仅当变量已定义时为真

    \#ifndef     //当且仅当变量已定义时为真

    

    \#endif      //检查结果为真，则执行到endif为止 



    \#ifndef SALES\_DATA\_H

    \#define SALES\_DATA\_H

    \#include &lt;string&gt;

    struct Sales\_data{

        std::string bookNo;

        unsigned units\_sold = 0;

        double revenue = 0.0;

    };

    \#endif



\*\*空指针:\*\*  



以往程序使用名为NULL的预处理变量（这个变量在头文件cstdlib中定义，值为0）；  



在C++11新标准中最好使用nullptr，同时尽量避免使用NULL，如：  



    int \*p = nullptr;





\#\# 其他



\#\#\# C++中的struct和class的区别



&gt; http://blog.sina.com.cn/s/blog\_48f587a80100k630.html



\* 最本质\(唯一\)的一个区别就是默认的访问控制  

1）默认的继承访问权限。struct是public的，class是private的。  

2）struct作为数据结构的实现体，它默认的数据访问控制是public的，而class作为对象的实现体，它默认的成员变量访问控制是private的。



\* 总的来说，struct更适合看成是一个数据结构的实现体，class更适合看成是一个对象的实现体。





C/C++中struct和class的区别：



&gt; http://genwoxuec.blog.51cto.com/1852764/503334



\#\#\# struct和typedef struct





&gt; http://www.cnblogs.com/qyaizs/articles/2039101.html

&gt; http://blog.csdn.net/haiou0/article/details/6877718

