
# Section 17 Interview Questions

## What are nullable types in C#? How do they differ from non-nullable types?

Nullable types in C# are value types that can also have a value of null. They are represented by adding a question mark '?' after the value type, such as int?, bool?, float?, etc. Non-nullable types, on the other hand, cannot have a value of null and do not require any special syntax.

## How do you use the Null Coalescing Operator in C#? Give an example.

The Null Coalescing Operator (??) in C# is used to provide a default value when a nullable value is null. It has the following syntax: valueToCheck ?? defaultValue. If the valueToCheck is null, it returns the defaultValue. Otherwise, it returns the valueToCheck.

### Example:

```csharp
int? nullableInt = null;
int defaultInt = 10;
int result = nullableInt ?? defaultInt;
```

In this example, if nullableInt is null, the value of defaultInt (which is 10) will be assigned to result.

## What is the null propagation operator in C#? How does it help in handling null values?

The null propagation operator (?.) in C# is used to access properties, methods, and indexers of an object without getting a null reference exception when the object is null. If the object is null, the expression with the null propagation operator will simply return null without throwing an exception.

### Example:

```csharp
class Person
{
    public string Name { get; set; }
    public int? Age { get; set; }
}

Person person = null;
string name = person?.Name; // Returns null
int? age = person?.Age; // Returns null
```

In this example, if person is null, both name and age will be assigned with null without throwing a null reference exception.

## What is NullReferenceException in C#?

NullReferenceException is a common exception that occurs in C# when you attempt to access a member (such as a property, method, or field) or invoke a method on an object that is null. In other words, it is an exception that is thrown when you try to perform an operation on an object reference that is not pointing to any object (i.e., is null).

### Example:

```csharp
string myString = null; // Assigning null to a string variable
int length = myString.Length; // Attempt to access Length property on a null object, which will throw NullReferenceException
```

In the above example, myString is assigned a value of null, which means it is not pointing to any object. When the Length property is accessed on myString, which is a member of the string class, a NullReferenceException will be thrown because myString is null and does not reference an actual object.

It's important to handle NullReferenceException properly in your code to ensure robustness and prevent unexpected crashes. This can be done by using defensive coding techniques, such as null checks, before accessing members or invoking methods on objects, as well as initializing variables properly to avoid uninitialized variables that may result in null references.

## How can you check if the value is null, before invoking a method of an object?

You can check if a value is null before invoking a method of an object in C# using the null conditional operator (?.) or null coalescing operator (??) in combination with an if statement.

### Example:

```csharp
MyClass myObject = GetMyObject(); // GetMyObject() returns an instance of MyClass or null
if (myObject != null)
{
    myObject.MyMethod(); // Invoke MyMethod only if myObject is not null
}
```

Alternatively, you can use the null conditional operator (?.) to directly invoke the method on the object and the method will only be invoked if the object is not null.

### Example:

```csharp
MyClass myObject = GetMyObject(); // GetMyObject() returns an instance of MyClass or null
myObject?.MyMethod(); // Invoke MyMethod only if myObject is not null
```

In this case, if myObject is null, the method MyMethod() will not be invoked, and no exception will be thrown.

You can also use the null coalescing operator (??) to provide a default value or perform some other action if the object is null.

### Example:

```csharp
MyClass myObject = GetMyObject(); // GetMyObject() returns an instance of MyClass or null
myObject?.MyMethod() ?? DefaultMethod();
```

In this case, if myObject is null, the DefaultMethod() will be invoked instead.

## What are best practices of handling null values in C#, to avoid NullReferenceException?

Handling null values properly is important in C# to avoid NullReferenceException and ensure robust and error-free code. Here are some best practices for handling null values in C#:

- **Use Nullable Value Types**: Use nullable value types (e.g., int?) instead of non-nullable value types (e.g., int) when you expect a value to be potentially null. This allows you to explicitly represent the possibility of null values and handle them accordingly.
- **Check for Nulls**: Always check for nulls before accessing properties, methods, or indexers of objects that may be null, using null conditional operator (?.) or null coalescing operator (??). This helps prevent NullReferenceException.
  - Example: `string result = myObject?.SomeProperty ?? "Default Value";`
- **Initialize Variables**: Initialize variables properly, especially reference types, to default values or appropriate initial values, to avoid uninitialized variables that may result in null references.
- **Use Defensive Coding Techniques**: Use defensive coding techniques, such as null checks and argument validation, to ensure that the input parameters or objects you are working with are not null before proceeding with any operations that may throw NullReferenceException.
- **Use Null Object Pattern**: Consider using the Null Object Pattern, where you create a special "null" object that represents the absence of a value instead of using actual null values. This can help avoid null checks and simplify your code.
- **Handle Exceptions Gracefully**: If you do encounter a null reference and an exception is thrown, handle it gracefully using try-catch blocks, logging, or other error-handling mechanisms to provide meaningful feedback to users and prevent application crashes.
- **Follow Coding Standards**: Follow coding standards and guidelines that advocate for defensive coding practices, including proper handling of null values, to ensure consistent and robust code across your project or team.

By following these best practices, you can effectively handle null values in C# and reduce the likelihood of encountering NullReferenceException or other related issues in your code.
