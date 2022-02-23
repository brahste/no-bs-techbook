# Generic Types, Traits, and Lifetimes

# Defining Generic Types

Similar to how duplicated code is a great indicator for where to create a function, some duplicated code can be reformatted to use generics.

You can define a generic type parameter to a function, e.g.:
```rust
fn func<T>(list: &[T]) -> T {...}
```
This function (`func`) is generic over the type `T` and has a single parameter names `list` which is a slice of values of type `Ti`. 

Note that if the functions with generic types won't compile if the logic isn't supported for all types that `T` could take on. In this case you have to specify the trait of the generic type as a parameter.

You can define a generic type parameter in a `struct`, e.g.:
```rust
struct Point<T> {
    x: T,
    y: T,
}
```
If you want to have different members of the `struct` to have different types, this can be achieved by specifying two generic types: `struct Point<T, U> {...}`

Enums can also have generic types. The `Option<T>` and `Result<T, E>` are two examples that are familiar to Rustaceans.
```rust
enum Option<T> {
    Some(T),
    None
}

enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Finally, you can specify generic types on methods implemented on structs.

[Fill out, see https://doc.rust-lang.org/book/ch10-01-syntax.html]


# Defining Traits to Manage Shared Behaviour

Traits serve the purpose of interfaces in other programming languages with a few differences.

## Default Implementations

If a trait has a method that is given some default behaviour then this default can be imposed an a `struct` that implements the trait. Simply don't provide any other implementation in the `impl` block and a the `struct` will take on the default methods.

```rust
trait Run {
    fn run(&self) -> String {
        String::from("Going for a run")
    }
}

pub struct Athlete {
    pub name: String,
}

impl Run for Athelete {}

let athelete = Athelete { name: String::from("Johnson") };
println!("The athelete {} is {}", athelete.name, athelete.run()); 
```
Output:
```
The athelete Johnson is Going for a run
```

__Note__: In the above example this is similar in essence to the role that a base implementation of a parent class in other languages such as C++.

## Traits as Parameters
You can define a function that takes a parameter that implements a specific trait. This allows the function to call methods on it's parameter, allowing potentially different types to be passed to the function. For example,

```rust
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}
```
In this example a type for `item` isn't specified, rather a trait is specified such that only arguments that implement the `Summary` trait are accepted.

# Validating References with Lifetimes

Every reference in Rust has a lifetime.
Lifetimes are specified as generics.
Lifetimes are meant to restrict access to dangling references

Rust employs a _borrow checker_ to validate the lifetimes of borrows to ensure they're used in the correct scope.

If you create a function that conditionally returns a reference (e.g. a string slice governed by and if/else) then the borrow checker doesn't know the lifetime of the returned value. In this case a lifetime specifier must be used.

The lifetime annotation syntax follows as such:

```rust
&i32         // a reference
&'a i32      // a reference with an explicit lifetime
&'a must i32 // a mutable reference with an explicit lifetime
```

Lifetime annotations tell Rust how generic lifetime parameters of multiple references relate to each other, so on their own they don't mean much without having another reference to compare to.
Since lifetime parameters are generics, they are specified inside angle brackets in function signatures. For example,

```rust
fn purchase_longest<'a>(item1: &'a str, item2: &'a str) -> &'a str {
   if item1.len() > item2.len()
        item1
    else
        item2
}
```

The above lifetime parameters declare that the returned value will live at least as long as the shortest living function parameter also annotated with the lifetime specifier `'a`.
It it important to understand that lifetime specifiers don't change the lifetime of the references, but place constraints on what the borrow checker uses to determine the useable scope of those references.
When returning a reference from a function, the lifetime parameter for the return type needs to match the lifetime parameter for one of the parameters.

Structs can also had attributes that are references by specifying a lifetime parameter.

```rust
struct Novel<'a> {
    paragraph1: &'a str,
    paragraph2: &'a str,
}
```

In this case, the struct `Novel` can't outlive the reference it holds.

---

A thought on references: For any concrete (instantiated) data type, there exists a location in memory that holds the value of that type. When we create a new variable with reference to that instance, we create a semantic abstraction where two variables access the same peice of memory. This is different than a pointer because a pointer holds the memory address of the associated instance. A reference doesn't only _point_ to that memory address, but creates a duplicate variable that borrows the value held _at_ the memory address. (In Rust) If the original instance goes out of scope then the memory location is freed automatically. If any references still exist to that memory address then a dangling reference would occur. Rust doesn't allow these to occur in the first place, so they have to be managed by the programmer pro-actively, instead of reactively as is the case in other programming languages.

---

Stopped at Lifetime Elision...
