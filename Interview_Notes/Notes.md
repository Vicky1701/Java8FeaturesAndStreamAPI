# Java 8 Functional Programming Guide

## 1. Functional Interfaces

### Core Functional Interfaces

#### Predicate
Represents a boolean-valued function, primarily used for filtering.
```java
Predicate<Integer> isEven = num -> num % 2 == 0;
System.out.println(isEven.test(4)); // true
```

#### Consumer
Accepts a single input and returns no result. Used for side effects.
```java
Consumer<String> print = str -> System.out.println(str);
print.accept("Hello"); // Prints "Hello"
```

#### Function
Represents a function that accepts one argument and produces a result.
```java
Function<String, Integer> length = str -> str.length();
System.out.println(length.apply("Java")); // 4
```

#### Supplier
Represents a supplier of results. Does not take any input.
```java
Supplier<Double> random = () -> Math.random();
System.out.println(random.get()); // Random double value
```

#### UnaryOperator
Represents an operation on a single operand that produces a result of the same type.
```java
UnaryOperator<Integer> square = num -> num * num;
System.out.println(square.apply(5)); // 25
```

#### BinaryOperator
Represents an operation on two operands of the same type, producing a result of the same type.
```java
BinaryOperator<Integer> add = (a, b) -> a + b;
System.out.println(add.apply(3, 5)); // 8
```

#### BiPredicate
Represents a predicate with two arguments.
```java
BiPredicate<String, Integer> isLengthEqual = (str, len) -> str.length() == len;
System.out.println(isLengthEqual.test("Java", 4)); // true
```

#### BiFunction
Represents a function that accepts two arguments and produces a result.
```java
BiFunction<Integer, Integer, String> concat = (a, b) -> a + " " + b;
System.out.println(concat.apply(3, 5)); // "3 5"
```

## 2. Streams API

### allMatch
Checks if all elements of the stream satisfy a given predicate.
```java
boolean allEven = numbers.stream().allMatch(n -> n % 2 == 0);
```

### anyMatch
Checks if any element of the stream satisfies a given predicate.
```java
boolean anyEven = numbers.stream().anyMatch(n -> n % 2 == 0);
```

### comparingInt
Used for sorting elements based on an integer property.
```java
numbers.sort(Comparator.comparingInt(n -> n));
```

### skip & limit
Skips the first `n` elements and limits the stream to `m` elements.
```java
numbers.stream().skip(2).limit(3).forEach(System.out::println);
```

### takeWhile & dropWhile
`takesWhile` returns elements until the predicate is false, `dropWhile` skips elements until the predicate is false.
```java
numbers.stream().takeWhile(n -> n < 4).forEach(System.out::println);
numbers.stream().dropWhile(n -> n < 4).forEach(System.out::println);
```

### Finding top, max, min, findFirst, and findAny
Finds elements in a stream.
```java
Optional<Integer> max = numbers.stream().max(Integer::compare);
Optional<Integer> min = numbers.stream().min(Integer::compare);
Optional<Integer> first = numbers.stream().findFirst();
Optional<Integer> any = numbers.stream().findAny();
```

### Sum, average, count
Performs aggregate operations on numeric streams.
```java
int sum = numbers.stream().mapToInt(Integer::intValue).sum();
double avg = numbers.stream().mapToInt(Integer::intValue).average().orElse(0);
long count = numbers.stream().count();
```

### Grouping by
Groups elements of a stream by a classifier function.
```java
Map<Integer, List<Integer>> grouped = numbers.stream().collect(Collectors.groupingBy(n -> n % 2));
```

## Quick Tips
1. Use `Predicate` for filtering conditions
2. Use `Consumer` for operations that don't return a value
3. Use `Function` for transformations
4. Use Streams API for processing collections in a functional style
5. Use `Collectors` to accumulate results into collections
6. Use Method References to simplify lambda expressions

