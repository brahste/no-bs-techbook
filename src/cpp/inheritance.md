# Classes and Inheritance

Inheritance is a fundamental component of any object oriented programming language such as C++.

## Access Modifiers

There are three access modifiers used in C++ classes: `public`, `private`, and `protected`.

- `public`: Members that are public are accessible everywhere inside the program.
- `private`: Members that are privated are accessible only within the class which they were defined.
- `protected`: Members that are protected are accessible in the class where they were defined _and_ any class that inherits from that class.

Note that if private or protected members of a class need to be accessed elsewhere in the program, this can be done by exposing those members through public methods. Getters and setters are an example of this.

### Tips, Tricks, and Hints

- If you're creating a variable that takes a template parameter then the class that you pass to the variable type can also be any of its inherited class.

For example:

```C++
std::unordered_map<std::string, CustomBaseClass> map;

CustomChildClass ccc = CustomChildClass();
// In the next line a CustomChildClass can be passed since it inherits from CustomBaseClass
map.insert(std::pair<std::string, CustomChildClass>("a", ccc)); 
```
## Virtual Inheritance
*Virtual inheritance* enforces that only one copy of a base class's members will be inherited in a grandchild class (second-level derivative).
> Links:
> - https://www.sandordargo.com/blog/2020/12/23/virtual-inheritance
