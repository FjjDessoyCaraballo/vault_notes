The `virtual` keyword in C++ is used primarily to enable **runtime polymorphism**, allowing derived classes to override base class methods and ensuring the correct method is called for the object, even when accessed through a base class pointer or reference.

### **Key Uses of `virtual`**

1. **Declaring Virtual Functions**:
    
    - A virtual function allows derived classes to override a method from the base class. When a function is declared as `virtual` in a base class, the function to call is determined dynamically (at runtime) based on the type of the object that the pointer or reference refers to, not the type of the pointer/reference itself.
2. **Virtual Destructor**:
    
    - A destructor should be declared `virtual` in a base class if it is intended to be polymorphic, to ensure proper cleanup when deleting derived class objects through a base class pointer.

### 1. Declaring Virtual Functions
#### Without `virtual` keyword

```cpp
#include <iostream>
using namespace std;

class Base 
{
	public:
	    void print() 
	    { 
		    cout << "Base class" << endl;
		}
};

class Derived : public Base 
{
	public:
	    void print()
	    { 
		    cout << "Derived class" << endl;
		}
};

int main() 
{
    Base* obj = new Derived();
    obj->print();
    delete obj;
    return 0;
}
```

After writing down our test in a file `test.cpp` we can check the output.

```shell
 fdessoy@fdessoy-420  ~  c++ test.cpp
 fdessoy@fdessoy-420  ~  ./a.out
Base class
```

- Expected output: "Derived class"

- Actual output: "Base class"

#### With `virtual` keyword

```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void print() { cout << "Base class" << endl; }
};

class Derived : public Base {
public:
    void print() override { cout << "Derived class" << endl; }
};

int main() {
    Base* obj = new Derived();
    obj->print();
    delete obj;
    return 0;
}
```

After writing down our test in a file `test.cpp` we can check the output.

```shell
 fdessoy@fdessoy-420  ~/projects/cpp_modules/cpp05   main  c++ test.cpp
 fdessoy@fdessoy-420  ~/projects/cpp_modules/cpp05   main  ./a.out
Derived class
```

- Expected output from `test.cpp`: "Derived class"

- Actual output from `test.cpp`: "Derived class" 

### 2. Virtual destructors

#### Without a virtual destructor

If you delete a derived class object through a base class pointer and the destructor is not virtual, the base class's destructor is called, which may lead to resource leaks.

```cpp
#include <iostream>
using namespace std;

class Base 
{
	public:
	    ~Base()
	    {
		    cout << "Base destroyed" << endl;
	    }
};

class Derived : public Base
{
	private:
	    int* data;
	public:
	    Derived() 
	    { 
	        data = new int[10];
	        cout << "Derived constructed and allocated 10 ints" << endl;
		}
	    ~Derived()
	    { 
	        delete[] data;
	        cout << "Derived destroyed and memory freed" << endl; 
	    }
};

int main()
{
    Base* obj = new Derived(); // Allocate a Derived object through a Base pointer
    delete obj; // Only Base's destructor is called, Derived's destructor is skipped
    return 0;
}
```

After writing down our test in a file `test.cpp` we can check the output.

```shell
 fdessoy@fdessoy-420  ~/projects/cpp_modules/cpp05   main  ./a.out 
Derived constructed and allocated 10 ints
Base destroyed
```

- Expected output in `test.cpp`:

- Actual output in `test.cpp`: 

```shell
==29967== HEAP SUMMARY:
==29967==     in use at exit: 40 bytes in 1 blocks
==29967==   total heap usage: 4 allocs, 3 frees, 74,800 bytes allocated
==29967== 
==29967== LEAK SUMMARY:
==29967==    definitely lost: 40 bytes in 1 blocks
==29967==    indirectly lost: 0 bytes in 0 blocks
==29967==      possibly lost: 0 bytes in 0 blocks
==29967==    still reachable: 0 bytes in 0 blocks
==29967==         suppressed: 0 bytes in 0 blocks
==29967== Rerun with --leak-check=full to see details of leaked memory
==29967== 
==29967== For lists of detected and suppressed errors, rerun with: -s
==29967== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
```

As it is possible to observe with the printouts from terminal, the derived class was not destroyed properly, and since we allocated memory within our derived class, all that memory was lost with it. The easy fix for this situation is to add the keyword `virtual` into our `base` class destructor.
#### With a virtual destructor

```cpp
#include <iostream>
using namespace std;

class Base 
{
	public:
	    virtual ~Base()
	    {
		    cout << "Base destroyed" << endl;
		}
};

class Derived : public Base 
{
	private:
	    int* data;
	public:
	    Derived()
	    { 
	        data = new int[10];
	        cout << "Derived constructed and allocated 10 ints" << endl;
	    }
	    ~Derived()
	    { 
	        delete[] data;
	        cout << "Derived destroyed and memory freed" << endl; 
	    }
};

int main()
{
    Base* obj = new Derived(); // Allocate a Derived object through a Base pointer
    delete obj; // Only Base's destructor is called, Derived's destructor is skipped
    return 0;
}
```

After writing down our test in a file `test.cpp` we can check the output.

```shell
 fdessoy@fdessoy-420  ~/projects/cpp_modules/cpp05   main  c++ test.cpp
 fdessoy@fdessoy-420  ~/projects/cpp_modules/cpp05   main  ./a.out
Derived constructed and allocated 10 ints
Derived destroyed and memory freed
Base destroyed
```

- Expected output in `test.cpp`:

- Actual output in `test.cpp`:

```shell
==32151== HEAP SUMMARY:
==32151==     in use at exit: 0 bytes in 0 blocks
==32151==   total heap usage: 4 allocs, 4 frees, 74,808 bytes allocated
==32151== 
==32151== All heap blocks were freed -- no leaks are possible
==32151== 
==32151== For lists of detected and suppressed errors, rerun with: -s
==32151== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

#### When to Use `virtual`

- Use `virtual` for functions in base classes when you expect derived classes to provide their own implementations.
- Use `virtual` destructors when a class is intended to be used polymorphically.