# Using Lambdas
Structure of a lambda in C++
```C++
[] () mutable throw() -> int {
	// ...lambda body
}
```

### Capture Clause
A lambda expression begins with a *capture clause*, which captures variables from its envrionment for use in the lambda expression. A capture clause is specified with `[]` and should specify the variables being used in the lambda.

There are three specific wildcard types that are useful when specifying capture clauses.
1. `[]` means the lambda doesn't take any variables from its environment.
2. `[=]` means that all variables that are used are captured by value.
3. `[&]` means that all variables that are used are captured by reference.

**Example**
All of the below capture clauses are equivalent
```C++
[&variable1, variable2]
[&, variable2]
[=, &variable1]
```
