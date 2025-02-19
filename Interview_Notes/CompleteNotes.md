# Introduction to Java 8 Features

## Overview of Java 8 Features
Java 8 introduced several new features to enhance the language, improve performance, and make coding more efficient. Some key features include:

- **Lambda Expressions** – Enables functional programming and reduces boilerplate code.
- **Functional Interfaces** – Predefined interfaces such as `Predicate`, `Function`, `Consumer`, etc.
- **Stream API** – Allows functional-style operations on collections.
- **Default & Static Methods in Interfaces** – Enables method implementations in interfaces.
- **Optional Class** – Handles null values more gracefully.
- **New Date and Time API** – Introduces `java.time` package for better date handling.
- **Collectors and Method References** – Simplifies data processing in Streams.

## Benefits of Functional Programming in Java
Java 8 brings functional programming paradigms that provide several benefits:

- **Concise Code** – Reduces verbosity, making code more readable.
- **Improved Readability & Maintainability** – Functional-style code is easier to understand.
- **Better Parallel Processing** – The Stream API supports parallel execution.
- **Encapsulation of Behavior** – Lambda expressions encapsulate behavior, making code more flexible.
- **Enhanced Performance** – Lazy evaluation and optimizations improve efficiency.

# Lambda Expressions in Java 8

## Introduction to Functional Programming in Java

### What is Functional Programming?
Functional programming is a programming paradigm where functions are treated as first-class citizens. This means:
- Functions can be assigned to variables
- Functions can be passed as arguments to other functions
- Functions can return other functions

Java 8 introduced functional programming through **Lambda Expressions** and the **Stream API**.

### Benefits of Using Lambda Expressions
Lambda expressions offer several advantages:
- **Concise and Readable Code** – Reduces boilerplate by eliminating anonymous classes
- **Improved Maintainability** – Functional-style code is easier to understand
- **Enhanced Performance** – Helps in writing parallel and optimized operations with the Stream API
- **Encapsulation of Behavior** – Allows passing behavior as parameters (higher-order functions)

## Syntax and Usage of Lambda Expressions

### Basic Syntax
Lambda expressions allow writing shorter and more expressive code. The syntax follows:

```java
(parameters) -> expression
```

or

```java
(parameters) -> { statements; }
```

### Examples of Lambda Expressions

#### 1. Lambda Expression for a Simple Function
```java
// Traditional way using an anonymous class
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello, world!");
    }
};

// Lambda expression version
Runnable r2 = () -> System.out.println("Hello, world!");

r1.run();
r2.run();
```

#### 2. Lambda Expression for a Custom Functional Interface
```java
@FunctionalInterface
interface MathOperation {
    int operation(int a, int b);
}

public class LambdaExample {
    public static void main(String[] args) {
        // Addition using lambda
        MathOperation addition = (a, b) -> a + b;
        
        // Multiplication using lambda
        MathOperation multiplication = (a, b) -> a * b;

        System.out.println("Addition: " + addition.operation(10, 5));
        System.out.println("Multiplication: " + multiplication.operation(10, 5));
    }
}
```

#### 3. Using Lambda Expressions with Streams
```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using lambda to print all names
        names.forEach(name -> System.out.println(name));
    }
}
```

## Functional Interfaces (@FunctionalInterface)

### What is a Functional Interface?
A functional interface is an interface with only one abstract method. It can have multiple default or static methods.

Example of a Functional Interface:
```java
@FunctionalInterface
interface Greeting {
    void sayHello();
}
```

### Predefined Functional Interfaces in Java 8
Java 8 provides several commonly used functional interfaces in the `java.util.function` package.

| Functional Interface | Description | Example |
|---------------------|-------------|----------|
| Runnable | Represents a task with no input and no output (void run()) | `Runnable r = () -> System.out.println("Running!");` |
| Consumer<T> | Takes an input but returns nothing (void accept(T t)) | `Consumer<String> printer = s -> System.out.println(s);` |
| Supplier<T> | Returns a value but takes no input (T get()) | `Supplier<Double> random = () -> Math.random();` |
| Predicate<T> | Takes an input and returns a boolean (boolean test(T t)) | `Predicate<Integer> isEven = n -> n % 2 == 0;` |
| Function<T, R> | Takes an input and returns a result (R apply(T t)) | `Function<Integer, String> intToString = num -> "Number: " + num;` |

### Example of Predefined Functional Interfaces
```java
import java.util.function.*;

public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        // Using Predicate
        Predicate<Integer> isEven = n -> n % 2 == 0;
        System.out.println("Is 4 even? " + isEven.test(4));

        // Using Function
        Function<String, Integer> lengthFunction = str -> str.length();
        System.out.println("Length of 'Hello': " + lengthFunction.apply("Hello"));

        // Using Consumer
        Consumer<String> printer = s -> System.out.println("Message: " + s);
        printer.accept("Hello, Functional Programming!");

        // Using Supplier
        Supplier<Double> randomSupplier = () -> Math.random();
        System.out.println("Random number: " + randomSupplier.get());
    }
}
```

### Custom Functional Interface Example
You can create your own functional interface with `@FunctionalInterface` annotation.

```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

public class CustomFunctionalInterfaceExample {
    public static void main(String[] args) {
        // Defining lambda expressions for different operations
        MathOperation addition = (a, b) -> a + b;
        MathOperation subtraction = (a, b) -> a - b;
        
        System.out.println("Sum: " + addition.operate(10, 5));
        System.out.println("Difference: " + subtraction.operate(10, 5));
    }
}
```

# Method References in Java 8

## Introduction to Method References
Method references are a shorthand notation for lambda expressions when calling existing methods. They improve code readability and reusability.

**Syntax:**  
```java
ClassName::methodName     // For static methods
objectName::methodName    // For instance methods
ClassName::new           // For constructor references
```

## 1. Static Method References (ClassName::staticMethod)
A static method reference is used when we want to call a static method.

### Example 1: Using a Static Method Reference
```java
import java.util.function.Function;

public class StaticMethodRefExample {
    public static int square(int num) {
        return num * num;
    }

    public static void main(String[] args) {
        // Using lambda expression
        Function<Integer, Integer> lambdaSquare = num -> StaticMethodRefExample.square(num);

        // Using method reference
        Function<Integer, Integer> methodRefSquare = StaticMethodRefExample::square;

        System.out.println("Square of 5: " + methodRefSquare.apply(5));
    }
}
```

### Example 2: Using a Static Method Reference with Streams
```java
import java.util.Arrays;
import java.util.List;

public class StaticMethodRefExample2 {
    public static void print(String str) {
        System.out.println(str);
    }

    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using method reference instead of lambda
        names.forEach(StaticMethodRefExample2::print);
    }
}
```

## 2. Instance Method References (objectName::instanceMethod)
An instance method reference is used to call a method on a specific instance.

### Example 1: Using an Instance Method Reference
```java
import java.util.function.Consumer;

public class InstanceMethodRefExample {
    public void showMessage(String message) {
        System.out.println("Message: " + message);
    }

    public static void main(String[] args) {
        InstanceMethodRefExample instance = new InstanceMethodRefExample();

        // Using lambda expression
        Consumer<String> lambdaMessage = msg -> instance.showMessage(msg);

        // Using method reference
        Consumer<String> methodRefMessage = instance::showMessage;

        methodRefMessage.accept("Hello, Method References!");
    }
}
```

### Example 2: Using an Instance Method Reference with Streams
```java
import java.util.Arrays;
import java.util.List;

public class InstanceMethodRefExample2 {
    public void display(String name) {
        System.out.println("Hello, " + name);
    }

    public static void main(String[] args) {
        InstanceMethodRefExample2 instance = new InstanceMethodRefExample2();
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Using method reference instead of lambda
        names.forEach(instance::display);
    }
}
```

## 3. Constructor References (ClassName::new)
A constructor reference is used when we need to create a new instance of a class.

### Example 1: Constructor Reference for Object Creation
```java
import java.util.function.Supplier;

class Sample {
    public Sample() {
        System.out.println("Sample Constructor Called!");
    }
}

public class ConstructorRefExample {
    public static void main(String[] args) {
        // Using lambda expression
        Supplier<Sample> lambdaConstructor = () -> new Sample();

        // Using constructor reference
        Supplier<Sample> constructorRef = Sample::new;

        constructorRef.get();  // Creates an instance of Sample
    }
}
```

### Example 2: Constructor Reference with Parameterized Constructor
```java
import java.util.function.Function;

class Person {
    private String name;

    public Person(String name) {
        this.name = name;
        System.out.println("Person created: " + name);
    }
}

public class ConstructorRefExample2 {
    public static void main(String[] args) {
        // Using lambda expression
        Function<String, Person> lambdaPerson = name -> new Person(name);

        // Using constructor reference
        Function<String, Person> constructorRef = Person::new;

        constructorRef.apply("Alice");
    }
}
```

# Default and Static Methods in Interfaces (Java 8)

## Introduction
Before Java 8, interfaces could only have abstract methods. Java 8 introduced **default methods** and **static methods** to provide additional functionalities without breaking existing implementations.

## Default Methods in Interfaces

### Why Default Methods?
- Allows adding new methods to interfaces without affecting classes that already implement them
- Helps avoid breaking changes in large applications
- Supports backward compatibility

### Syntax of Default Methods
```java
interface MyInterface {
    default void show() {
        System.out.println("Default method in interface");
    }
}
```

### Example: Using Default Methods
```java
interface Vehicle {
    default void start() {
        System.out.println("Vehicle is starting...");
    }
}

class Car implements Vehicle {
    // Car does not need to override start() unless required
}

public class DefaultMethodExample {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start(); // Calls default method in Vehicle interface
    }
}
```

### Resolving Multiple Inheritance Issues

#### Problem: Diamond Problem with Default Methods
If a class implements multiple interfaces that define the same default method, it leads to ambiguity.

```java
interface A {
    default void show() {
        System.out.println("A's show method");
    }
}

interface B {
    default void show() {
        System.out.println("B's show method");
    }
}

class C implements A, B {
    // Compilation error: show() is defined in both A and B
}
```

#### Solution: Override the Conflicting Method
```java
class C implements A, B {
    @Override
    public void show() {
        System.out.println("Overriding to resolve conflict");
    }
}
```

Or explicitly choose a parent interface:
```java
class C implements A, B {
    @Override
    public void show() {
        A.super.show(); // Calls A's version of show()
    }
}
```

## Static Methods in Interfaces

### Why Static Methods?
- Allows defining utility/helper methods inside interfaces
- Eliminates the need for separate utility classes

### Syntax of Static Methods
```java
interface MathUtil {
    static int square(int num) {
        return num * num;
    }
}
```

### Example: Using Static Methods in Interfaces
```java
interface MathOperations {
    static int add(int a, int b) {
        return a + b;
    }
}

public class StaticMethodExample {
    public static void main(String[] args) {
        int result = MathOperations.add(5, 3);
        System.out.println("Sum: " + result);
    }
}
```

## Key Differences Between Default and Static Methods

| Feature | Default Methods | Static Methods |
|---------|----------------|----------------|
| Invocation | Called on an instance (`obj.method()`) | Called on the interface (`InterfaceName.method()`) |
| Overriding | Can be overridden in implementing classes | Cannot be overridden |
| Purpose | Add new behavior to interfaces without breaking existing implementations | Provide utility/helper methods |


# Java 8 Features

## 5. Optional Class

### Why Use Optional?
`Optional<T>` helps avoid `NullPointerException` by providing a way to handle optional values.

### Creating an Optional
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> opt = Optional.of("Hello");  // Non-null value
        Optional<String> emptyOpt = Optional.empty(); // Empty Optional
    }
}
```

### Common Methods

| Method | Description |
|--------|-------------|
| `of(T value)` | Creates an Optional with a non-null value. Throws NullPointerException if null. |
| `ofNullable(T value)` | Creates an Optional that can hold null values. |
| `isPresent()` | Returns true if a value is present, false otherwise. |
| `ifPresent(Consumer<T>)` | Executes a function if the value is present. |
| `orElse(T other)` | Returns the value if present, otherwise returns other. |
| `orElseGet(Supplier<T>)` | Returns the value if present, otherwise executes Supplier. |
| `orElseThrow(Supplier<Throwable>)` | Returns the value if present, otherwise throws an exception. |

### Example Usage
```java
import java.util.Optional;

public class OptionalExample {
    public static void main(String[] args) {
        Optional<String> opt = Optional.ofNullable(null);

        // isPresent
        System.out.println("Is present? " + opt.isPresent());

        // ifPresent
        opt.ifPresent(value -> System.out.println("Value: " + value));

        // orElse
        System.out.println("Default: " + opt.orElse("Default Value"));

        // orElseGet
        System.out.println("Generated: " + opt.orElseGet(() -> "Generated Value"));

        // orElseThrow
        opt.orElseThrow(() -> new RuntimeException("Value not found!"));
    }
}
```

## 6. Date and Time API (java.time Package)

### Introduction
Java 8 introduced the `java.time` package to replace `java.util.Date` and `java.util.Calendar`.

### 1. LocalDate, LocalTime, LocalDateTime, ZonedDateTime
```java
import java.time.*;

public class DateTimeExample {
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        LocalTime time = LocalTime.now();
        LocalDateTime dateTime = LocalDateTime.now();
        ZonedDateTime zonedDateTime = ZonedDateTime.now();

        System.out.println("LocalDate: " + date);
        System.out.println("LocalTime: " + time);
        System.out.println("LocalDateTime: " + dateTime);
        System.out.println("ZonedDateTime: " + zonedDateTime);
    }
}
```

### 2. Duration and Period
Duration is used for time differences.
Period is used for date differences.

```java
import java.time.*;

public class DurationPeriodExample {
    public static void main(String[] args) {
        Duration duration = Duration.ofHours(5);
        Period period = Period.ofDays(10);

        System.out.println("Duration: " + duration);
        System.out.println("Period: " + period);
    }
}
```

### 3. DateTimeFormatter for Formatting
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class DateTimeFormatterExample {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");
        
        String formattedDate = now.format(formatter);
        System.out.println("Formatted Date: " + formattedDate);
    }
}
```

## 7. Nashorn JavaScript Engine

### Introduction
Nashorn allows executing JavaScript inside Java applications.

### Example: Running JavaScript in Java
```java
import javax.script.*;

public class NashornExample {
    public static void main(String[] args) throws ScriptException {
        ScriptEngine engine = new ScriptEngineManager().getEngineByName("Nashorn");
        engine.eval("print('Hello from JavaScript!');");
    }
}
```

### Example: JavaScript Function Execution
```java
import javax.script.*;

public class NashornFunctionExample {
    public static void main(String[] args) throws ScriptException, NoSuchMethodException {
        ScriptEngine engine = new ScriptEngineManager().getEngineByName("Nashorn");
        engine.eval("function greet(name) { return 'Hello, ' + name; }");

        Invocable invocable = (Invocable) engine;
        String result = (String) invocable.invokeFunction("greet", "Alice");
        System.out.println(result);
    }
}
```

## 8. Type Annotations

### Introduction
Java 8 allows annotations on any type (not just classes or methods).

### Example: @NonNull Type Annotation
```java
import javax.annotation.Nonnull;

public class TypeAnnotationExample {
    public void greet(@Nonnull String name) {
        System.out.println("Hello, " + name);
    }

    public static void main(String[] args) {
        new TypeAnnotationExample().greet(null);  // This will cause a warning
    }
}
```

## 9. Repeating Annotations

### Introduction
Java 8 allows using the same annotation multiple times on a single element.

### Defining a Repeating Annotation
```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@Repeatable(MyAnnotations.class)
@interface MyAnnotation {
    String value();
}

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface MyAnnotations {
    MyAnnotation[] value();
}
```

### Applying Repeating Annotations
```java
@MyAnnotation("First")
@MyAnnotation("Second")
public class RepeatingAnnotationExample {
    public static void main(String[] args) {
        MyAnnotation[] annotations = RepeatingAnnotationExample.class
            .getAnnotationsByType(MyAnnotation.class);
        for (MyAnnotation annotation : annotations) {
            System.out.println(annotation.value());
        }
    }
}
```

# Stream API (Java 8)

## Introduction to Streams

### What is a Stream?
- A **Stream** is a sequence of elements that supports **functional-style** operations on collections
- It provides **lazy evaluation**, meaning computations are performed only when necessary

### Difference Between Streams and Collections
| Feature | Collections | Streams |
|---------|------------|----------|
| Storage | Stores elements | Does not store elements |
| Iteration | External iteration (for-each loop) | Internal iteration (functional) |
| Modification | Allows adding/removing elements | Cannot modify original source |
| Execution | Eager (executes immediately) | Lazy (executes only when needed) |

### Characteristics of Streams
1. **Lazy Evaluation** - Operations are evaluated only when a terminal operation is invoked
2. **Pipelining** - Intermediate operations return a stream, allowing method chaining
3. **Automatic Iteration** - Stream handles iteration internally

## Stream Creation

### Creating Streams from Collections
```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("apple", "banana", "cherry");
        Stream<String> stream = list.stream();  // Convert list to stream
        stream.forEach(System.out::println);
    }
}
```

### Other Creation Methods
```java
// From Arrays
Stream<Integer> stream = Arrays.stream(new Integer[]{1, 2, 3, 4});

// Using Stream.of()
Stream<String> stream = Stream.of("A", "B", "C");

// Using Stream.generate()
Stream<Double> randomNumbers = Stream.generate(Math::random).limit(5);

// Using Stream.iterate()
Stream<Integer> evenNumbers = Stream.iterate(0, n -> n + 2).limit(5);
```

## Intermediate Operations

### filter()
Filters elements based on a condition.
```java
list.stream()
    .filter(s -> s.startsWith("a"))
    .forEach(System.out::println);
```

### map()
Transforms elements.
```java
list.stream()
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

### flatMap()
Flattens nested collections.
```java
List<List<Integer>> numbers = Arrays.asList(
    Arrays.asList(1, 2), 
    Arrays.asList(3, 4)
);
numbers.stream()
    .flatMap(Collection::stream)
    .forEach(System.out::println);
```

### Other Intermediate Operations
```java
// distinct() - Removes duplicates
Stream.of(1, 2, 2, 3, 4)
    .distinct()
    .forEach(System.out::println);

// sorted() - Sorts elements
list.stream()
    .sorted()
    .forEach(System.out::println);

// peek() - For debugging
list.stream()
    .peek(System.out::println)
    .map(String::toUpperCase)
    .forEach(System.out::println);

// limit() - Limits elements
list.stream()
    .limit(2)
    .forEach(System.out::println);

// skip() - Skips elements
list.stream()
    .skip(1)
    .forEach(System.out::println);
```

### Java 9+ Operations
```java
// takeWhile()
Stream.of(1, 2, 3, 4, 5)
    .takeWhile(n -> n < 4)
    .forEach(System.out::println);

// dropWhile()
Stream.of(1, 2, 3, 4, 5)
    .dropWhile(n -> n < 4)
    .forEach(System.out::println);
```

## Terminal Operations

### Basic Terminal Operations
```java
// forEach()
list.stream().forEach(System.out::println);

// collect()
List<String> result = list.stream().collect(Collectors.toList());

// reduce()
int sum = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);

// count()
long count = list.stream().count();
```

### Finding Elements
```java
// min(), max()
Optional<String> min = list.stream().min(Comparator.naturalOrder());
Optional<String> max = list.stream().max(Comparator.naturalOrder());

// findFirst(), findAny()
Optional<String> first = list.stream().findFirst();
Optional<String> any = list.stream().findAny();
```

### Matching Operations
```java
boolean anyMatch = list.stream().anyMatch(s -> s.startsWith("a"));
boolean allMatch = list.stream().allMatch(s -> s.length() > 3);
boolean noneMatch = list.stream().noneMatch(s -> s.contains("z"));
```

## Collectors

### Basic Collection Operations
```java
// To List/Set/Map
List<String> resultList = list.stream().collect(Collectors.toList());
Set<String> resultSet = list.stream().collect(Collectors.toSet());
Map<Integer, String> resultMap = list.stream()
    .collect(Collectors.toMap(String::length, s -> s));

// Joining
String joined = list.stream().collect(Collectors.joining(", "));
```

### Grouping and Partitioning
```java
// groupingBy()
Map<Integer, List<String>> groupedByLength = list.stream()
    .collect(Collectors.groupingBy(String::length));

// partitioningBy()
Map<Boolean, List<String>> partitioned = list.stream()
    .collect(Collectors.partitioningBy(s -> s.startsWith("a")));
```

### Advanced Collectors
```java
// collectingAndThen()
List<String> immutableList = list.stream()
    .collect(Collectors.collectingAndThen(
        Collectors.toList(), 
        Collections::unmodifiableList
    ));

// Summary Statistics
IntSummaryStatistics stats = Stream.of(1, 2, 3, 4)
    .collect(Collectors.summarizingInt(Integer::intValue));
```

## Primitive Streams

### Basic Operations
```java
// Range operations
IntStream.range(1, 5).forEach(System.out::println);
IntStream.rangeClosed(1, 5).forEach(System.out::println);

// Statistics
int sum = IntStream.range(1, 5).sum();
OptionalDouble avg = IntStream.range(1, 5).average();
IntSummaryStatistics stats = IntStream.range(1, 5).summaryStatistics();

// Boxing
List<Integer> list = IntStream.range(1, 5)
    .boxed()
    .collect(Collectors.toList());
```

# Java 8 Functional Programming Guide

## Stream Operations

### Basic Stream Creation
```java
// Using Stream.of()
Stream<String> stream = Stream.of("Java", "Python", "C++");

// Using Arrays.stream()
int[] numbers = {1, 2, 3, 4, 5};
IntStream intStream = Arrays.stream(numbers);

// Using range operations
IntStream.range(1, 5);        // 1 to 4
IntStream.rangeClosed(1, 5);  // 1 to 5
```

### Stream Manipulation
```java
// Using iterate and limit
Stream.iterate(1, n -> n + 2)
    .limit(5)
    .peek(System.out::println);

// Converting to List
List<Integer> list = IntStream.range(1, 5)
    .boxed()
    .collect(Collectors.toList());

// String joining
List<String> words = Arrays.asList("Java", "Streams", "Functional");
String result = words.stream()
    .collect(Collectors.joining(", "));

// Flattening nested lists
List<List<String>> nestedList = Arrays.asList(
    Arrays.asList("A", "B"),
    Arrays.asList("C", "D")
);
List<String> flatList = nestedList.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList());
```

## Advanced Operations

### Finding Elements
```java
// Max and Min
Optional<Integer> max = Stream.of(1, 2, 3, 4).max(Integer::compareTo);
Optional<Integer> min = Stream.of(1, 2, 3, 4).min(Integer::compareTo);

// First and Any
Optional<Integer> first = Stream.of(1, 2, 3, 4).findFirst();
Optional<Integer> any = Stream.of(1, 2, 3, 4).findAny();
```

### Sorting and Grouping
```java
// Custom sorting
List<String> names = Arrays.asList("Bob", "Alice", "Charlie");
names.stream()
    .sorted(Comparator.comparingInt(String::length));

// Grouping
Map<Integer, List<String>> groupedByLength = names.stream()
    .collect(Collectors.groupingBy(String::length));

// Partitioning
Map<Boolean, List<String>> partitioned = names.stream()
    .collect(Collectors.partitioningBy(s -> s.startsWith("A")));
```

### Aggregate Operations
```java
IntSummaryStatistics stats = IntStream.of(1, 2, 3, 4, 5).summaryStatistics();
// Access via: stats.getSum(), stats.getAverage(), stats.getCount()
```

## Functional Interfaces

### Core Interfaces
```java
// Predicate - Returns boolean
Predicate<Integer> isEven = num -> num % 2 == 0;

// Consumer - Performs action
Consumer<String> print = System.out::println;

// Function - Converts input to output
Function<String, Integer> lengthFunction = String::length;

// Supplier - Provides value
Supplier<Double> randomSupplier = Math::random;

// UnaryOperator - Transforms value
UnaryOperator<Integer> square = x -> x * x;

// BinaryOperator - Operation on two values
BinaryOperator<Integer> sum = Integer::sum;

// BiPredicate - Tests two arguments
BiPredicate<Integer, String> checkLength = (num, str) -> str.length() == num;

// BiFunction - Takes two inputs, produces output
BiFunction<Integer, Integer, String> sumToString = (a, b) -> "Sum: " + (a + b);
```

### Primitive Functional Interfaces
- `IntBinaryOperator`: `(a, b) -> a + b`
- `IntConsumer`: `x -> System.out.println(x)`
- `IntFunction<R>`: `x -> "Number: " + x`
- `IntPredicate`: `x -> x > 0`
- `IntSupplier`: `() -> 42`
- `IntToDoubleFunction`: `x -> x / 2.0`
- `IntToLongFunction`: `x -> x * 2L`
- `IntUnaryOperator`: `x -> x * x`

## Advanced Stream Operations

### Working with Custom Classes
```java
class Employee {
    String name;
    int age;
    
    Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

List<Employee> employees = Arrays.asList(
    new Employee("Alice", 30),
    new Employee("Bob", 25)
);

// Stream operations on custom objects
employees.stream()
    .map(emp -> emp.name)
    .forEach(System.out::println);
```

### Matching Operations
```java
boolean allAdults = employees.stream().allMatch(emp -> emp.age > 18);
boolean anyTeenager = employees.stream().anyMatch(emp -> emp.age < 20);
boolean noTeenager = employees.stream().noneMatch(emp -> emp.age < 20);
```

### Stream Slicing (Java 9+)
```java
// Skip and Limit
Stream.of(1, 2, 3, 4, 5)
    .skip(2)
    .limit(2);

// takeWhile and dropWhile
Stream.of(1, 2, 3, 4, 5)
    .takeWhile(n -> n < 4);  // 1, 2, 3
Stream.of(1, 2, 3, 4, 5)
    .dropWhile(n -> n < 4);  // 4, 5
```



