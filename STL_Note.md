# STL

## 组成

* 容器（containers）
* 算法（algorithms）
* 迭代器（iterators）
* 仿函数（functors）
* 配接器（adapters）
* 空间配置器（allocator）

## 容器（containers）

* 序列式容器（sequence containers）：元素都是可序（ordered），但未必是有序（sorted）
* 关联式容器（associattive containers）

### array

array是固定大小的顺序容器，它们保存了一个以严格的线性顺序排列的特定数量的元素。

在内部，一个数组除了它所包含的元素（甚至不是它的大小，它是一个模板参数，在编译时是固定的）以外不保存任何数据。存储大小与用语言括号语法（[]）声明的普通数组一样高效。这个类只是增加了一层成员函数和全局函数，所以数组可以作为标准容器使用。

与其他标准容器不同，数组具有固定的大小，并且不通过分配器管理其元素的分配：它们是封装固定大小数组元素的聚合类型。因此，他们不能动态地扩大或缩小。

零大小的数组是有效的，但是它们不应该被解除引用（成员的前面，后面和数据）。

与标准库中的其他容器不同，交换两个数组容器是一种线性操作，它涉及单独交换范围内的所有元素，这通常是相当低效的操作。另一方面，这允许迭代器在两个容器中的元素保持其原始容器关联。

数组容器的另一个独特特性是它们可以被当作元组对象来处理：array头部重载get函数来访问数组元素，就像它是一个元组，以及专门的tuple_size和tuple_element类型。

```
template < class T, size_t N > class array;
```

#### array::begin

返回指向数组容器中第一个元素的迭代器。

![](https://i.stack.imgur.com/oa3EQ.png)

```
      iterator begin() noexcept;
const_iterator begin() const noexcept;
```

Example

```
#include <iostream>
#include <array>

int main()
{
    std::array<int, 5> myarray = {2, 16, 77,34, 50};
    std::cout << "myarray contains:";
    for(auto it = myarray.begin(); it != myarray.end(); ++i)
        std::cout << ' ' << *it;
    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 2 16 77 34 50
```

#### array::end

返回指向数组容器中最后一个元素之后的理论元素的迭代器。

```
      iterator end() noexcept;
const_iterator end() const noexcept;
```

Example

```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,5> myarray = { 5, 19, 77, 34, 99 };

    std::cout << "myarray contains:";
    for ( auto it = myarray.begin(); it != myarray.end(); ++it )
        std::cout << ' ' << *it;

    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 5 19 77 34 99
```

#### array::rbegin

返回指向数组容器中最后一个元素的反向迭代器。

```
      reverse_iterator rbegin（）noexcept;
const_reverse_iterator rbegin（）const noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,4> myarray = {4, 26, 80, 14} ;
    for(auto rit = myarray.rbegin(); rit < myarray.rend(); ++rit)
        std::cout << ' ' << *rit;
    
    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 14 80 26 4
```

#### array::rend

返回一个反向迭代器，指向数组中第一个元素之前的理论元素（这被认为是它的反向结束）。

```
      reverse_iterator rend() noexcept;
const_reverse_iterator rend() const noexcept;
```

Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,4> myarray = {4, 26, 80, 14};
    std::cout << "myarray contains";
    for(auto rit = myarray.rbegin(); rit < myarray.rend(); ++rit)
        std::cout << ' ' << *rit;
    
    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 14 80 26 4
```

#### array::cbegin

返回指向数组容器中第一个元素的常量迭代器（const_iterator）；这个迭代器可以增加和减少，但是不能用来修改它指向的内容。
```
const_iterator cbegin（）const noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,5> myarray = {2, 16, 77, 34, 50};
    
    std::cout << "myarray contains:";

    for ( auto it = myarray.cbegin(); it != myarray.cend(); ++it )
        std::cout << ' ' << *it;   // cannot modify *it

    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 2 16 77 34 50
```

#### array::cend
返回指向数组容器中最后一个元素之后的理论元素的常量迭代器（const_iterator）。这个迭代器可以增加和减少，但是不能用来修改它指向的内容。
```
const_iterator cend() const noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,5> myarray = { 15, 720, 801, 1002, 3502 };

    std::cout << "myarray contains:";
    for ( auto it = myarray.cbegin(); it != myarray.cend(); ++it )
        std::cout << ' ' << *it;   // cannot modify *it

    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 2 16 77 34 50
```

#### array::crbegin
返回指向数组容器中最后一个元素的常量反向迭代器（const_reverse_iterator）
```
const_reverse_iterator crbegin（）const noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,6> myarray = {10, 20, 30, 40, 50, 60} ;

    std::cout << "myarray backwards:";
    for ( auto rit=myarray.crbegin() ; rit < myarray.crend(); ++rit )
        std::cout << ' ' << *rit;   // cannot modify *rit

    std::cout << '\n';

    return 0;
}
```
Output
```
myarray backwards: 60 50 40 30 20 10
```
#### array::crend

返回指向数组中第一个元素之前的理论元素的常量反向迭代器（const_reverse_iterator），它被认为是其反向结束。

```
const_reverse_iterator crend() const noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,6> myarray = {10, 20, 30, 40, 50, 60} ;

    std::cout << "myarray backwards:";
    for ( auto rit=myarray.crbegin() ; rit < myarray.crend(); ++rit )
        std::cout << ' ' << *rit;   // cannot modify *rit

    std::cout << '\n';

    return 0;
}
```
Output
```
myarray backwards: 60 50 40 30 20 10
```

#### array::size

返回数组容器中元素的数量。

```
constexpr size_type size（）noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,5> myints;
    std::cout << "size of myints:" << myints.size() << std::endl;
    std::cout << "sizeof(myints):" << sizeof(myints) << std::endl;

    return 0;
}
```
Possible Output
```
size of myints: 5
sizeof(myints): 20
```
#### array::max_size
返回数组容器可容纳的最大元素数。数组对象的max_size与其size一样，始终等于用于实例化数组模板类的第二个模板参数。
```
constexpr size_type max_size() noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,10> myints;
    std::cout << "size of myints: " << myints.size() << '\n';
    std::cout << "max_size of myints: " << myints.max_size() << '\n';

    return 0;
}
```
Output
```
size of myints: 10
max_size of myints: 10
```

#### array::empty
返回一个布尔值，指示数组容器是否为空，即它的size()是否为0。
```
constexpr bool empty() noexcept;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
  std::array<int,0> first;
  std::array<int,5> second;
  std::cout << "first " << (first.empty() ? "is empty" : "is not empty") << '\n';
  std::cout << "second " << (second.empty() ? "is empty" : "is not empty") << '\n';
  return 0;
}
```
Output:
```
first is empty
second is not empt
```
#### array::operator[]
返回数组中第n个位置的元素的引用。与array::at相似，但array::at会检查数组边界并通过抛出一个out_of_range异常来判断n是否超出范围，而array::operator[]不检查边界。
```
      reference operator[] (size_type n);
const_reference operator[] (size_type n) const;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,10> myarray;
    unsigned int i;

    // assign some values:
    for(i=0; i<10; i++)
        myarray[i] = i;

    // print content
    std::cout << "myarray contains:";
    for(i=0; i<10; i++)
        std::cout << ' ' << myarray[i];
    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 0 1 2 3 4 5 6 7 8 9
```
#### array::at
返回数组中第n个位置的元素的引用。与array::operator[]相似，但array::at会检查数组边界并通过抛出一个out_of_range异常来判断n是否超出范围，而array::operator[]不检查边界。
```
      reference at ( size_type n );
const_reference at ( size_type n ) const;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
    std::array<int,10> myarray;
    unsigned int i;

    // assign some values:
    for(i=0; i<10; i++)
        myarray[i] = i;

    // print content
    std::cout << "myarray contains:";
    for(i=0; i<10; i++)
        std::cout << ' ' << myarray[i];
    std::cout << '\n';

    return 0;
}
```
Output
```
myarray contains: 0 1 2 3 4 5 6 7 8 9
```
#### array::front
返回对数组容器中第一个元素的引用。array::begin返回的是迭代器，array::front返回的是直接引用。  
在空容器上调用此函数会导致未定义的行为。
```
      reference front();
const_reference front() const;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
  std::array<int,3> myarray = {2, 16, 77};

  std::cout << "front is: " << myarray.front() << std::endl;   // 2
  std::cout << "back is: " << myarray.back() << std::endl;     // 77

  myarray.front() = 100;

  std::cout << "myarray now contains:";
  for ( int& x : myarray ) std::cout << ' ' << x;

  std::cout << '\n';

  return 0;
}
```
Output
```
front is: 2
back is: 77
myarray now contains: 100 16 77
```
#### array::back
返回对数组容器中最后一个元素的引用。array::end返回的是迭代器，array::back返回的是直接引用。  
在空容器上调用此函数会导致未定义的行为。
```
      reference back();
const_reference back() const;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
  std::array<int,3> myarray = {5, 19, 77};

  std::cout << "front is: " << myarray.front() << std::endl;   // 5
  std::cout << "back is: " << myarray.back() << std::endl;     // 77

  myarray.back() = 50;

  std::cout << "myarray now contains:";
  for ( int& x : myarray ) std::cout << ' ' << x;
  std::cout << '\n';

  return 0;
}
```
Output
```
front is: 5
back is: 77
myarray now contains: 5 19 50
```
#### array::data
返回指向数组对象中第一个元素的指针。

由于数组中的元素存储在连续的存储位置，所以检索到的指针可以偏移以访问数组中的任何元素。
```
      value_type* data() noexcept;
const value_type* data() const noexcept;
```
Example
```
#include <iostream>
#include <cstring>
#include <array>

int main ()
{
  const char* cstr = "Test string";
  std::array<char,12> charray;

  std::memcpy (charray.data(),cstr,12);

  std::cout << charray.data() << '\n';

  return 0;
}
```
Output
```
Test string
```
#### array::fill
用val填充数组所有元素，将val设置为数组对象中所有元素的值。
```
void fill (const value_type& val);
```
Example
```
#include <iostream>
#include <array>

int main () {
  std::array<int,6> myarray;

  myarray.fill(5);

  std::cout << "myarray contains:";
  for ( int& x : myarray) { std::cout << ' ' << x; }

  std::cout << '\n';

  return 0;
}
```
Output
```
myarray contains: 5 5 5 5 5 5
```
#### array::swap
通过x的内容交换数组的内容，这是另一个相同类型的数组对象（包括相同的大小）。

与其他容器的交换成员函数不同，此成员函数通过在各个元素之间执行与其大小相同的单独交换操作，以线性时间运行。
```
void swap (array& x) noexcept(noexcept(swap(declval<value_type&>(),declval<value_type&>())));
```
Example
```
#include <iostream>
#include <array>

int main ()
{
  std::array<int,5> first = {10, 20, 30, 40, 50};
  std::array<int,5> second = {11, 22, 33, 44, 55};

  first.swap (second);

  std::cout << "first:";
  for (int& x : first) std::cout << ' ' << x;
  std::cout << '\n';

  std::cout << "second:";
  for (int& x : second) std::cout << ' ' << x;
  std::cout << '\n';

  return 0;
}
```
Output
```
first: 11 22 33 44 55
second: 10 20 30 40 50
```
#### get（array）
形如：std::get<0>(myarray)；传入一个数组容器，返回指定位置元素的引用。
```
template <size_t I，class T，size_t N> T＆get（array <T，N>＆arr）noexcept; 
template <size_t I，class T，size_t N> T && get（array <T，N> && arr）noexcept; 
template <size_t I，class T，size_t N> const T＆get（const array <T，N>＆arr）noexcept;
```
Example
```
#include <iostream>
#include <array>
#include <tuple>

int main ()
{
  std::array<int,3> myarray = {10, 20, 30};
  std::tuple<int,int,int> mytuple (10, 20, 30);

  std::tuple_element<0,decltype(myarray)>::type myelement;  // int myelement

  myelement = std::get<2>(myarray);
  std::get<2>(myarray) = std::get<0>(myarray);
  std::get<0>(myarray) = myelement;

  std::cout << "first element in myarray: " << std::get<0>(myarray) << "\n";
  std::cout << "first element in mytuple: " << std::get<0>(mytuple) << "\n";

  return 0;
}
```
Output
```
first element in myarray: 30
first element in mytuple: 10
```
#### relational operators (array)
形如：arrayA != arrayB、arrayA > arrayB；依此比较数组每个元素的大小关系。
```
（1）	
template <class T，size_T N> 
  bool operator ==（const array <T，N>＆lhs，const array <T，N>＆rhs）;
（2）	
template <class T，size_T N> 
  bool operator！=（const array <T，N>＆lhs，const array <T，N>＆rhs）;
（3）	
template <class T，size_T N> 
  bool operator <（const array <T，N>＆lhs，const array <T，N>＆rhs）;
（4）	
template <class T，size_T N> 
  bool operator <=（const array <T，N>＆lhs，const array <T，N>＆rhs）;
（5）	
template <class T，size_T N> 
  bool operator>（const array <T，N>＆lhs，const array <T，N>＆rhs）;
（6）	
template <class T，size_T N> 
  bool operator> =（const array <T，N>＆lhs，const array <T，N>＆rhs）;
```
Example
```
#include <iostream>
#include <array>

int main ()
{
  std::array<int,5> a = {10, 20, 30, 40, 50};
  std::array<int,5> b = {10, 20, 30, 40, 50};
  std::array<int,5> c = {50, 40, 30, 20, 10};

  if (a==b) std::cout << "a and b are equal\n";
  if (b!=c) std::cout << "b and c are not equal\n";
  if (b<c) std::cout << "b is less than c\n";
  if (c>b) std::cout << "c is greater than b\n";
  if (a<=b) std::cout << "a is less than or equal to b\n";
  if (a>=b) std::cout << "a is greater than or equal to b\n";

  return 0;
}
```
Output
```
a and b are equal
b and c are not equal
b is less than c
c is greater than b
a is less than or equal to b
a is greater than or equal to b
```
### vector
vector是表示可以改变大小的数组的序列容器。

就像数组一样，vector为它们的元素使用连续的存储位置，这意味着它们的元素也可以使用到其元素的常规指针上的偏移来访问，而且和数组一样高效。但是与数组不同的是，它们的大小可以动态地改变，它们的存储由容器自动处理。

在内部，vector使用一个动态分配的数组来存储它们的元素。这个数组可能需要重新分配，以便在插入新元素时增加大小，这意味着分配一个新数组并将所有元素移动到其中。就处理时间而言，这是一个相对昂贵的任务，因此每次将元素添加到容器时矢量都不会重新分配。

相反，vector容器可以分配一些额外的存储以适应可能的增长，并且因此容器可以具有比严格需要包含其元素（即，其大小）的存储更大的实际容量。库可以实现不同的策略的增长到内存使用和重新分配之间的平衡，但在任何情况下，再分配应仅在对数生长的间隔发生尺寸，使得在所述载体的末端各个元件的插入可以与提供分期常量时间复杂性。

因此，与阵列相比，载体消耗更多的内存来交换管理存储和以有效方式动态增长的能力。

与其他动态序列容器（deques，lists和 forward\_lists ）相比，vector非常有效地访问其元素（就像数组一样），并相对有效地从元素末尾添加或移除元素。对于涉及插入或移除除了结尾之外的位置的元素的操作，它们执行比其他位置更差的操作，并且具有比列表和 forward\_lists 更不一致的迭代器和引用。

```
template < class T, class Alloc = allocator<T> > class vector;
```

#### vector::vector
（1）empty容器构造函数（默认构造函数）
构造一个空的容器，没有元素。
（2）fill构造函数
用n个元素构造一个容器。每个元素都是val的副本（如果提供）。
（3）范围（range）构造器
使用与[ range，first，last]范围内的元素相同的顺序构造一个容器，其中的每个元素都是emplace -从该范围内相应的元素构造而成。
（4）复制（copy）构造函数（并用分配器复制）
按照相同的顺序构造一个包含x中每个元素的副本的容器。
（5）移动（move）构造函数（和分配器移动）
构造一个获取x元素的容器。
如果指定了alloc并且与x的分配器不同，那么元素将被移动。否则，没有构建元素（他们的所有权直接转移）。
x保持未指定但有效的状态。
（6）初始化列表构造函数
构造一个容器中的每个元件中的一个拷贝的IL，以相同的顺序。

```
default (1)	
explicit vector (const allocator_type& alloc = allocator_type());
fill (2)	
explicit vector (size_type n);
         vector (size_type n, const value_type& val,
                 const allocator_type& alloc = allocator_type());
range (3)	
template <class InputIterator>
  vector (InputIterator first, InputIterator last,
          const allocator_type& alloc = allocator_type());
copy (4)	
vector (const vector& x);
vector (const vector& x, const allocator_type& alloc);
move (5)	
vector (vector&& x);
vector (vector&& x, const allocator_type& alloc);
initializer list (6)	
vector (initializer_list<value_type> il,
       const allocator_type& alloc = allocator_type());
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
    // constructors used in the same order as described above:
    std::vector<int> first;             // empty vector of ints
    std::vector<int> second(4, 100);    // four ints with value 100
    std::vector<int> third(second.begin(), second.end());// iterating through second
    std::vector<int> fourth(third);     // a copy of third

    // the iterator constructor can also be used to construct from arrays:
    int myints[] = {16,2,77,29};
    std::vector<int> fifth(myints, myints + sizeof(myints) / sizeof(int));

    std::cout << "The contents of fifth are:";
    for(std::vector<int>::iterator it = fifth.begin(); it != fifth.end(); ++it)
        std::cout << ' ' << *it;
    std::cout << '\n';

    return 0;
}
```
Output
```
The contents of fifth are: 16 2 77 29 
```
#### vector::~vector
销毁容器对象。这将在每个包含的元素上调用allocator_traits::destroy，并使用其分配器释放由矢量分配的所有存储容量。
```
~vector();
```
#### vector::operator=
将新内容分配给容器，替换其当前内容，并相应地修改其大小。
```
copy (1)	
vector& operator= (const vector& x);
move (2)	
vector& operator= (vector&& x);
initializer list (3)	
vector& operator= (initializer_list<value_type> il);
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> foo (3,0);
  std::vector<int> bar (5,0);

  bar = foo;
  foo = std::vector<int>();

  std::cout << "Size of foo: " << int(foo.size()) << '\n';
  std::cout << "Size of bar: " << int(bar.size()) << '\n';
  return 0;
}
```
Output
```
Size of foo: 0
Size of bar: 3
```
#### vector::begin
#### vector::end
#### vector::rbegin
#### vector::rend
#### vector::cbegin
#### vector::cend
#### vector::rcbegin
#### vector::rcend
#### vector::size

返回vector中元素的数量。

这是vector中保存的实际对象的数量，不一定等于其存储容量。

```
size_type size() const noexcept;
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myints;
  std::cout << "0. size: " << myints.size() << '\n';

  for (int i=0; i<10; i++) myints.push_back(i);
  std::cout << "1. size: " << myints.size() << '\n';

  myints.insert (myints.end(),10,100);
  std::cout << "2. size: " << myints.size() << '\n';

  myints.pop_back();
  std::cout << "3. size: " << myints.size() << '\n';

  return 0;
}
```
Output
```
0. size: 0
1. size: 10
2. size: 20
3. size: 19
```
#### vector::max_size
返回该vector可容纳的元素的最大数量。由于已知的系统或库实现限制，

这是容器可以达到的最大潜在大小，但容器无法保证能够达到该大小：在达到该大小之前的任何时间，仍然无法分配存储。
```
size_type max_size() const noexcept;
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector;

  // set some content in the vector:
  for (int i=0; i<100; i++) myvector.push_back(i);

  std::cout << "size: " << myvector.size() << "\n";
  std::cout << "capacity: " << myvector.capacity() << "\n";
  std::cout << "max_size: " << myvector.max_size() << "\n";
  return 0;
}
```
A possible output for this program could be:
```
size: 100
capacity: 128
max_size: 1073741823
```
#### vector::resize
调整容器的大小，使其包含n个元素。

如果n小于当前的容器size，内容将被缩小到前n个元素，将其删除（并销毁它们）。

如果n大于当前容器size，则通过在末尾插入尽可能多的元素以达到大小n来扩展内容。如果指定了val，则新元素将初始化为val的副本，否则将进行值初始化。

如果n也大于当前的容器的capacity（容量），分配的存储空间将自动重新分配。

注意这个函数通过插入或者删除元素的内容来改变容器的实际内容。
```
void resize (size_type n);
void resize (size_type n, const value_type& val);
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector;

  // set some initial content:
  for (int i=1;i<10;i++) myvector.push_back(i);

  myvector.resize(5);
  myvector.resize(8,100);
  myvector.resize(12);

  std::cout << "myvector contains:";
  for (int i=0;i<myvector.size();i++)
    std::cout << ' ' << myvector[i];
  std::cout << '\n';

  return 0;
}
```
Output
```
myvector contains: 1 2 3 4 5 100 100 100 0 0 0 0
```
#### vector::capacity
返回当前为vector分配的存储空间的大小，用元素表示。这个capacity(容量)不一定等于vector的size。它可以相等或更大，额外的空间允许适应增长，而不需要重新分配每个插入。
```
size_type capacity() const noexcept;
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector;

  // set some content in the vector:
  for (int i=0; i<100; i++) myvector.push_back(i);

  std::cout << "size: " << (int) myvector.size() << '\n';
  std::cout << "capacity: " << (int) myvector.capacity() << '\n';
  std::cout << "max_size: " << (int) myvector.max_size() << '\n';
  return 0;
}
```
A possible output for this program could be:
```
size: 100
capacity: 128
max_size: 1073741823
```
#### vector::empty
返回vector是否为空（即，它的size是否为0）
```
bool empty() const noexcept;
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector;
  int sum (0);

  for (int i=1;i<=10;i++) myvector.push_back(i);

  while (!myvector.empty())
  {
     sum += myvector.back();
     myvector.pop_back();
  }

  std::cout << "total: " << sum << '\n';

  return 0;
}
```
Output
```
total: 55
```
#### vector::reserve
请求vector容量至少足以包含n个元素。

如果n大于当前vector容量，则该函数使容器重新分配其存储容量，从而将其容量增加到n（或更大）。

在所有其他情况下，函数调用不会导致重新分配，并且vector容量不受影响。

这个函数对vector大小没有影响，也不能改变它的元素。
```
void reserve (size_type n);
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int>::size_type sz;

  std::vector<int> foo;
  sz = foo.capacity();
  std::cout << "making foo grow:\n";
  for (int i=0; i<100; ++i) {
    foo.push_back(i);
    if (sz!=foo.capacity()) {
      sz = foo.capacity();
      std::cout << "capacity changed: " << sz << '\n';
    }
  }

  std::vector<int> bar;
  sz = bar.capacity();
  bar.reserve(100);   // this is the only difference with foo above
  std::cout << "making bar grow:\n";
  for (int i=0; i<100; ++i) {
    bar.push_back(i);
    if (sz!=bar.capacity()) {
      sz = bar.capacity();
      std::cout << "capacity changed: " << sz << '\n';
    }
  }
  return 0;
}
```
Possible output
```
making foo grow:
capacity changed: 1
capacity changed: 2
capacity changed: 4
capacity changed: 8
capacity changed: 16
capacity changed: 32
capacity changed: 64
capacity changed: 128
making bar grow:
capacity changed: 100
```
#### vector::shrink_to_fit
要求容器减小其capacity(容量)以适应其尺寸。

该请求是非绑定的，并且容器实现可以自由地进行优化，并且保持capacity大于其size的vector。 这可能导致重新分配，但对矢量大小没有影响，并且不能改变其元素。
```
void shrink_to_fit();
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector (100);
  std::cout << "1. capacity of myvector: " << myvector.capacity() << '\n';

  myvector.resize(10);
  std::cout << "2. capacity of myvector: " << myvector.capacity() << '\n';

  myvector.shrink_to_fit();
  std::cout << "3. capacity of myvector: " << myvector.capacity() << '\n';

  return 0;
}
```
Possible output
```
1. capacity of myvector: 100
2. capacity of myvector: 100
3. capacity of myvector: 10
```
#### vector::operator[]
#### vector::at
#### vector::front
#### vector::back
#### vector::data

#### vector::assign
将新内容分配给vector，替换其当前内容，并相应地修改其大小。

在范围版本（1）中，新内容是从第一个和最后一个范围内的每个元素按相同顺序构造的元素。

在填充版本（2）中，新内容是n个元素，每个元素都被初始化为一个val的副本。

在初始化列表版本（3）中，新内容是以相同顺序作为初始化列表传递的值的副本。

所述内部分配器被用于（通过其性状），以分配和解除分配存储器如果重新分配发生。它也习惯于摧毁所有现有的元素，并构建新的元素。
```
range (1)	
template <class InputIterator>
  void assign (InputIterator first, InputIterator last);
fill (2)	
void assign (size_type n, const value_type& val);
initializer list (3)	
void assign (initializer_list<value_type> il);
```
Example
```
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> first;
  std::vector<int> second;
  std::vector<int> third;

  first.assign (7,100);             // 7 ints with a value of 100

  std::vector<int>::iterator it;
  it=first.begin()+1;

  second.assign (it,first.end()-1); // the 5 central values of first

  int myints[] = {1776,7,4};
  third.assign (myints,myints+3);   // assigning from array.

  std::cout << "Size of first: " << int (first.size()) << '\n';
  std::cout << "Size of second: " << int (second.size()) << '\n';
  std::cout << "Size of third: " << int (third.size()) << '\n';
  return 0;
}
```
Output
```
Size of first: 7
Size of second: 5
Size of third: 3
```

补充：vector::assign 与 vector::operator= 的区别：
1. vector::assign 实现源码
```cpp
void assign(size_type __n, const _Tp& __val) { _M_fill_assign(__n, __val); }

template <class _Tp, class _Alloc>
void vector<_Tp, _Alloc>::_M_fill_assign(size_t __n, const value_type& __val) 
{
  if (__n > capacity()) {
    vector<_Tp, _Alloc> __tmp(__n, __val, get_allocator());
    __tmp.swap(*this);
  }
  else if (__n > size()) {
    fill(begin(), end(), __val);
    _M_finish = uninitialized_fill_n(_M_finish, __n - size(), __val);
  }
  else
    erase(fill_n(begin(), __n, __val), end());
}
```
2. vector::operator= 实现源码
```cpp
template <class _Tp, class _Alloc>
vector<_Tp,_Alloc>& 
vector<_Tp,_Alloc>::operator=(const vector<_Tp, _Alloc>& __x)
{
  if (&__x != this) {
    const size_type __xlen = __x.size();
    if (__xlen > capacity()) {
      iterator __tmp = _M_allocate_and_copy(__xlen, __x.begin(), __x.end());
      destroy(_M_start, _M_finish);
      _M_deallocate(_M_start, _M_end_of_storage - _M_start);
      _M_start = __tmp;
      _M_end_of_storage = _M_start + __xlen;
    }
    else if (size() >= __xlen) {
      iterator __i = copy(__x.begin(), __x.end(), begin());
      destroy(__i, _M_finish);
    }
    else {
      copy(__x.begin(), __x.begin() + size(), _M_start);
      uninitialized_copy(__x.begin() + size(), __x.end(), _M_finish);
    }
    _M_finish = _M_start + __xlen;
  }
  return *this;
}
```
### deque

### forward_list

### list

### stack

### queue

### priority_queue

### set

### multiset

### map

### multimap

### unordered_set 

### unordered_multiset 

### unordered_map 

### unordered_multimap 



