# Best Practices

> Links
> 
> - [C&#43;&#43; Return: std::any, std::optional, or std::variant? - C&#43;&#43; Stories](https://www.cppstories.com/2021/sphero-cpp-return/#result-based-on-stdvariant)

1. If you use it, include it, don't depend on headers including each other.

2. **(Note that the destructor of must be virtual, as is the case for all classes you intend to inherit from - otherwise the destructor of the derived class will not be called when you delete an object through a base pointer, and you’ll get corrupted program states like memory leaks.)**
3. You should make a function virtual only when there is a valid reason for a subclass to override it.

## Virtual Destructors
> Always make a base class's destructor virtual and public, or non-vritual and protected.
> - [Virtuality](http://www.gotw.ca/publications/mill18.htm)

**Example**
Say you create a base class `Parent` that has virtual methods and a derived class `Child` that inherits from base. 
```C++
class Parent {
	~Parent(){}
	// virtual methods
}

class Child : public Parent {
	~Child() {
		// clean up
	}
}
```
Using the polymorphism of C++ you can create a concrete dervied class through a pointer to the base class.
```C++
Parent *p = new Child();
delete p;
```
In this case only the destructor of `Parent` is called, because that's the static type. Since the destructor of `Child` won't be called, a memory leak can occur.

To resolve this issue, always make the base class's destructor virtual.