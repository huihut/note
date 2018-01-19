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

```
template < class T, size_t N > class array;
```

#### array::begin

返回指向数组容器中第一个元素的迭代器。

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

![](https://i.stack.imgur.com/oa3EQ.png)

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
### vector

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



