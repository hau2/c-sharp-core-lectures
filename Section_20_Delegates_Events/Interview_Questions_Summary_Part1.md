
# Section 20 Interview Questions - Part 1

## What are Delegates in C#? Explain their purpose and usage.
A Delegate is a type in C# that represents a reference to a method. It allows you to pass methods as parameters, store them in variables, and invoke them dynamically at runtime.
Delegates are commonly used for event handling, callback functions, and implementing design patterns like the observer pattern.

## Can you explain the different types of Delegates in C#?
There are two types of Delegates in C#:
- **Singlecast Delegate**: Points to a single method and can invoke only one method at a time.
- **Multicast Delegate**: Can point to multiple methods and invoke them in a sequence or in parallel. Used for implementing events in C#.

## Explain Events in C# and their purpose in real-world projects.
Events in C# provide notifications when certain actions or conditions occur in an application. They allow classes to communicate with each other in a loosely coupled manner. Events are used to handle user interactions, respond to changes in state, and implement the observer pattern in projects.

## What are Auto-implemented Events in C#?
Auto-implemented Events are a shorthand syntax for creating events with a default implementation for the add and remove blocks. Introduced in C# 3.0, they allow you to define events using just the event keyword, without explicitly defining the underlying delegate or the add/remove blocks.
```csharp
public event EventHandler MyEvent;
```
This automatically creates a private backing field for the event and generates default add and remove blocks.

## What are Anonymous Methods in C#? How are they used?
Anonymous Methods are unnamed methods that can be defined inline in C# code. Introduced in C# 2.0, they simplify the creation of small, short-lived methods used as event handlers or delegates.
```csharp
button.Click += delegate(object sender, EventArgs e)
{
  // Event handler implementation
};
```
This example uses an Anonymous Method as the event handler for a button's Click event.

## Explain Lambda Expressions in C# and their usage in real-world projects.
Lambda Expressions are a shorthand syntax for creating anonymous methods in C#. Introduced in C# 3.0, they provide a concise way to write small, inline functions used as event handlers, in LINQ queries, and more.
```csharp
button.Click += (sender, e) =>
{
  // Event handler implementation
};
```
This example uses a Lambda Expression as the event handler for a button's Click event.

## What are Inline Lambda Expressions in C#? How are they used?
Inline Lambda Expressions are a shorthand syntax for using Lambda Expressions in contexts like LINQ queries or method calls. They allow you to define a Lambda Expression inline without explicitly specifying the delegate type.
```csharp
var result = myList.Where(item => item.Length > 5);
```
This example uses an Inline Lambda Expression in a LINQ query to filter a list.

## What are Expression Trees in C#? How are they used?
Expression Trees in C# represent code as data, allowing you to inspect, analyze, and transform expressions at runtime. They are used for implementing dynamic code generation, querying databases, and building dynamic queries.
Expression Trees represent lambda expressions and other expressions in a tree-like structure, where each node represents an operation, such as an operator or a method call.

## Explain Switch Expression in C# and its usage.
Switch Expression in C# is an enhanced version of the traditional switch statement introduced in C# 8.0. It provides a concise way to write switch-like behavior using expressions instead of statements.
```csharp
string color = "red";
string result = color switch
{
    "red" => "Stop",
    "yellow" => "Caution",
    "green" => "Go",
    _ => "Unknown"
};
```
This example uses a Switch Expression to determine the traffic light status based on the color.

## Real-world project scenario using Delegates, Events, Lambda expressions, Switch expressions, and Expression bodied methods
Imagine building a multi-threaded data processing application for sensors in a factory. Use Delegates, Events, and Lambda Expressions to handle data from different sensors concurrently.

### Steps:
1. Define a custom delegate for processing sensor data.
2. Define events for each type of sensor.
3. Create event handlers using Lambda Expressions.
4. Use Auto-implemented Events to raise events.
5. Use Lambda Expressions to define inline event handlers.
6. Use expression-bodied members for concise code.
7. Use switch expressions to route data to corresponding event handlers.
```csharp
// Define delegate
public delegate void SensorDataProcessor(object data);

// Define events in sensor classes
public class TemperatureSensor
{
    public event SensorDataProcessor TemperatureDataReceived;
    public void ReceiveData(object data) => TemperatureDataReceived?.Invoke(data);
}

// Subscribe to events with Lambda Expressions
TemperatureSensor.TemperatureDataReceived += async (data) =>
{
    await ProcessTemperatureDataAsync(data);
};

// Use switch expressions for routing
switch (dataType)
{
    case DataType.Temperature:
        TemperatureSensor.TemperatureDataReceived?.Invoke(data);
        break;
    case DataType.Pressure:
        PressureSensor.PressureDataReceived?.Invoke(data);
        break;
    case DataType.Humidity:
        HumiditySensor.HumidityDataReceived?.Invoke(data);
        break;
    default:
        // Handle unknown data type
        break;
}
```
By combining these features, you can efficiently process data from multiple sources concurrently, making the code more modular, extensible, and maintainable.
