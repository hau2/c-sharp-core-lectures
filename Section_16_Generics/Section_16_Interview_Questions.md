
# Section 16 Interview Questions

## What are generic classes in C#? Provide an example of how to define and use a generic class.
Generic classes are classes that allow the use of type parameters to define the data types that they work with. They are defined using the "class" keyword followed by the type parameter(s) enclosed in angle brackets <>.

### Example:
```csharp
class Stack<T>
{
    private T[] items;
    // Implementation of Stack class...
}

// To use a generic class:
Stack<int> intStack = new Stack<int>();
intStack.Push(1);
intStack.Push(2);
intStack.Push(3);
```

## What are generic methods in C#? Provide an example of how to define and use a generic method.
Generic methods are methods that can work with different data types using type parameters. They are defined using the same syntax as generic classes, but with the type parameter(s) declared at the method level, enclosed in angle brackets <>.

### Example:
```csharp
class Helper
{
    public T Max<T>(T a, T b) where T : IComparable<T>
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}

// To use a generic method:
Helper helper = new Helper();
int result = helper.Max(5, 10);
```

## What are generic constraints in C#? Why are they important?
Generic constraints are used to restrict the type parameters that can be used with generic classes or methods. They specify the requirements that a type must satisfy in order to be used as a type argument. Generic constraints are important because they help ensure type safety and provide better compile-time checking.

### Types of generic constraints in C#:
- `where T : struct`: restricts the type parameter to value types.
- `where T : class`: restricts the type parameter to reference types.
- `where T : new()`: restricts the type parameter to types that have a default constructor.
- `where T : SomeType`: restricts the type parameter to a specific type or its derived types.

## Can you provide an example of using generic constraints in a real-world project scenario?
Sure! Let's consider a scenario where you are building a data access layer for a web application (developed using Asp.Net MVC or Asp.Net Core), and you want to create a generic repository class that can work with different entities in the application, such as Customer, Order, and Product. You can use generic constraints to ensure that the entities used as type arguments implement a specific interface, such as IEntity, which defines common properties like Id and CreatedAt.

### Example:
```csharp
interface IEntity
{
    int Id { get; set; }
    DateTime CreatedAt { get; set; }
}

class Repository<T> where T : IEntity
{
    public void Insert(T entity)
    {
        // Implementation of insert operation...
    }

    public void Update(T entity)
    {
        // Implementation of update operation...
    }

    public void Delete(T entity)
    {
        // Implementation of delete operation...
    }

    public T GetById(int id)
    {
        // Implementation of get by ID operation...
    }
}
```

In this example, the `Repository<T>` class has a generic type parameter `T` that is constrained to implement the `IEntity` interface, ensuring that only entities that implement this interface can be used as type arguments. This provides type safety and ensures that the methods in the `Repository` class can only be used with entities that have the required properties.

## How can you specify multiple generic constraints for a type parameter in C#?
You can specify multiple generic constraints for a type parameter in C# using the following syntax:
```csharp
where T : constraint1, constraint2, ...
```

### Example:
```csharp
class MyClass<T> where T : class, IFirstInterface, ISecondInterface
{
    // Implementation of MyClass...
}
```

## What is the purpose of the default keyword in generic constraints?
In C#, the `default` keyword is used as a constraint in generic type parameters to specify that the type argument must have a default (parameterless) constructor. This is known as the `new()` constraint.

### Example:
```csharp
class MyGenericClass<T> where T : new()
{
    // Implementation of MyGenericClass...
}
```

In this example, the `new()` constraint ensures that the type argument `T` has a default constructor, which allows you to create a new instance of `T` using `new T()`. If `T` does not have a default constructor, a compile-time error will occur.

The `default` keyword in generic constraints is useful in scenarios where you need to ensure that the type argument passed to a generic type or method can be instantiated with a default constructor, such as when you need to create new instances of the type within the generic class or method. It provides compile-time safety and helps prevent runtime errors related to missing default constructors.

## Can you explain the concept of type inference in C# with respect to generic methods?
Type inference in C# is the ability of the compiler to automatically determine the type arguments for a generic method based on the arguments passed to the method. This allows you to call a generic method without explicitly specifying the type arguments, making the code more concise and readable.

### Example:
```csharp
void PrintArray<T>(T[] arr)
{
    foreach (T item in arr)
    {
        Console.WriteLine(item);
    }
}

// Usage:
int[] numbers = { 1, 2, 3, 4, 5 };
string[] names = { "Alice", "Bob", "Charlie" };

PrintArray(numbers); // Type inference infers T as int
PrintArray(names);   // Type inference infers T as string
```

Type inference in C# works based on the types of the arguments passed to the method and the constraints specified on the generic type parameters. It simplifies the usage of generic methods and reduces the need for explicit type argument specifications, making the code more concise and less error-prone.
