
# Section 20 Interview Questions - Part 2

## How can Expression Trees be used in real-world projects. Explain with a sample scenario?
Expression Trees in C# represent expressions as data structures that can be inspected, analyzed, and manipulated at runtime. They are typically used in scenarios like code generation, query builders, and ORM frameworks.

### Example Scenario:
Imagine building an ORM framework that maps database tables to C# classes and allows querying data using LINQ-like syntax. You can use Expression Trees to dynamically compose queries at runtime.

```csharp
public class Query<T>
{
    private Expression<Func<T, bool>> _filter;

    public Query<T> Where(Expression<Func<T, bool>> predicate)
    {
        _filter = _filter == null ? predicate : _filter.And(predicate);
        return this;
    }

    public IQueryable<T> Execute()
    {
        var queryableData = GetQueryableData();
        return queryableData.Where(_filter);
    }
}

public static class ExpressionExtensions
{
    public static Expression<Func<T, bool>> And<T>(this Expression<Func<T, bool>> left, Expression<Func<T, bool>> right)
    {
        var parameter = left.Parameters.Single();
        var body = Expression.AndAlso(left.Body, right.Body.ReplaceParameter(right.Parameters.Single(), parameter));
        return Expression.Lambda<Func<T, bool>>(body, parameter);
    }
}
```

## How can you handle custom add/remove logic in C# events?
In C#, you can customize the add and remove logic of events by explicitly defining them.

### Example:
```csharp
public class EventExample
{
    private EventHandler _myEvent;

    public event EventHandler MyEvent
    {
        add
        {
            _myEvent += value;
            // Additional logic, if needed
        }
        remove
        {
            _myEvent -= value;
            // Additional logic, if needed
        }
    }
}
```

## What are the differences between anonymous methods and lambda expressions in C#?
### Syntax:
- **Anonymous methods** use the `delegate` keyword followed by a parameter list and a code block.
    ```csharp
    delegate (int x, int y)
    {
        // Code block
    };
    ```
- **Lambda expressions** use the `=>` syntax followed by an expression or a code block.
    ```csharp
    (int x, int y) => x + y;
    ```

### Type Inference:
- **Lambda expressions** automatically infer the parameter types and return type.
    ```csharp
    (x, y) => x + y;
    ```
- **Anonymous methods** require explicit type annotations.
    ```csharp
    delegate (int x, int y)
    {
        return x + y;
    };
    ```

### Usage with LINQ:
- **Lambda expressions** are commonly used with LINQ.
    ```csharp
    var result = myList.Where(item => item > 10);
    ```
- **Anonymous methods** are less commonly used with LINQ.
    ```csharp
    var result = myList.Where(delegate (int item)
    {
        return item > 10;
    });
    ```

## What are expression bodied members in C# and how are they used?
Expression bodied members in C# provide a concise way to define members using an expression instead of a full code block.

### Example:
```csharp
public class MyClass
{
    private int _value;

    // Expression bodied property
    public int Value
    {
        get => _value;
        set => _value = value;
    }

    // Expression bodied method
    public void PrintValue() => Console.WriteLine(_value);
}
```

## How can you use pre-defined delegates such as Func, Action, Predicate, and EventHandler in C#?
### Func<T>
Represents a delegate that takes parameters of type T and returns a value.
```csharp
Func<int, int, int> add = (x, y) => x + y;
int result = add(2, 3); // result is 5
```

### Action<T>
Represents a delegate that takes parameters of type T and does not return a value.
```csharp
Action<string> print = message => Console.WriteLine(message);
print("Hello, world!"); // Prints "Hello, world!"
```

### Predicate<T>
Represents a delegate that takes a parameter of type T and returns a boolean value.
```csharp
Predicate<int> isEven = number => number % 2 == 0;
bool result = isEven(4); // result is true
```

### EventHandler
Represents a delegate commonly used for handling events.
```csharp
public class MyEventArgs : EventArgs { }

public class MyClass
{
    public event EventHandler MyEvent;
    public event EventHandler<MyEventArgs> MyGenericEvent;

    private void OnMyEvent() => MyEvent?.Invoke(this, EventArgs.Empty);
    private void OnMyGenericEvent(MyEventArgs e) => MyGenericEvent?.Invoke(this, e);
}

var obj = new MyClass();
obj.MyEvent += (sender, args) => Console.WriteLine("MyEvent raised");
obj.OnMyEvent();
obj.MyGenericEvent += (sender, args) => Console.WriteLine($"MyGenericEvent raised with argument: {args}");
obj.OnMyGenericEvent(new MyEventArgs());
```

## Where to use Func, Action, Predicate in real world applications in C#?
### Func:
- **Data processing**: Transform or filter data.
- **Callbacks**: Define callback methods for asynchronous operations.
- **Dependency injection**: Provide factory methods.

### Action:
- **Event handling**: Define event handlers.
- **Asynchronous operations**: Define callbacks for asynchronous operations.

### Predicate:
- **Collection filtering**: Define conditions for filtering elements.
- **Validation**: Define validation rules for input data or business logic.

## What is the difference between lambda expressions and expression-bodied members?
### Lambda Expressions
Anonymous functions used to create inline delegate instances or short, concise blocks of code.
```csharp
Func<int, int, int> add = (a, b) => a + b;
```

### Expression-Bodied Members
Shorthand syntax for writing concise single-expression methods or properties.
```csharp
public int Square(int x) => x * x;
```

Lambda expressions are used for creating delegates, while expression-bodied members are used for defining methods or properties in C# classes.
