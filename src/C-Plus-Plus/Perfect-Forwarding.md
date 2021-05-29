### Basic Idea  

An **identifier** of which the **type** is the **rvalue reference** is still a **lvalue** since the identifier can be identified.  

### Example without Perfect Forwarding  

For example, the following code will fail when compiled.  

```c++
#include <utility>

void foo(int &&i)
{
    
}

int main()
{
    int i = 1;
    int &&r = std::move(i);

    foo(r);

    return 0;
}
```

```c++
main.cpp: In function ‘int main()’:
main.cpp:13:9: error: cannot bind rvalue reference of type ‘int&&’ to lvalue of type ‘int’
     foo(r);
         ^
main.cpp:3:6: note:   initializing argument 1 of ‘void foo(int&&)’
 void foo(int &&i)
```

### Example with Perfect Forwarding  

The "std::forward" can be used to fix the compilation error.

```c++
#include <utility>

void foo(int &&i)
{
    
}

int main()
{
    int i = 1;
    int &&r = std::move(i);

    foo(std::forward<decltype(r)>(r));

    return 0;
}
```