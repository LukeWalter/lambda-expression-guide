# Lambda Expression Implementation Guide

## Without Generics

1. Find the functional interface that you want to reference. Here's an example of a functional interface:

   ```java
   public interface SomeInterface {
      int myMethod(int x, int y);
   
   }
   ```java
   
   **NOTE:** The interface you're using can only have one abstract method. If there are more, then
   the compiler will no longer be able to infer the parameters and return type of the method
   you're trying to implement.
   
1. Use the reference type of your interface to create an object reference. This reference will contain
   your lambda expression. For this example, I'll call it `lambda`.
   
   ```java
   SomeInterface lambda;
   ```java
   
1. Identify the parameters (input) and return type (output) of the method in your interface.
   
   ```java
   int myMethod(int x, int y);
   ```java
   
   
   | Input | Output        |
   |-------|---------------|
   | `int x` | returns `int` |
   | `int y` |               |


1. Start building the lambda expression. The format is as follows:
   
   ```java
   ( parameters ) -> { function implementation; };
   ```java
   
1. In order to build a valid lambda expression for our `SomeInterface` reference, the following must be true:
   
   1.  The lambda must take in the same parameters as the method in `SomeInterface`.
   2.  The implementation in the body of the lambda must return with the same data type as 
       the method from `SomeInterface`.
   
   Because `myMethod` takes in two integers as inputs and returns an integer, our lambda expression will do the same.
   
   ```java
   SomeInterface lambda = (x, y) -> { return x + y; };
   ```java
   
   **NOTE** The types for x and y don't need to be explicitly stated in our lambda. If the compiler has access to the
   `SomeInterface` class, then it will already know what types of variables that `myMethod` should take in as parameters.
   As long as the **number** of parameters in your lambda expression is the same as the number of parameters in `myMethod`, 
   then the compiler will treat each parameter in the lambda as if they were the same data type as the respective parameters
   in `myMethod`.
   
   ```java
   SomeInterface lambda = (int x, int y) -> { return x + y; }; // This is the same as the lambda expression above!
   ```java
   
### Review

Using the `SomeInterface` functional interface, which of the following lambda expressions are valid?

1. `SomeInterface a = (x, y) -> { return x * y + x + 2; };`
1. `SomeInterface b = (x) -> { return x; };`
1. `SomeInterface c = (a, b) -> { return a + b; };`
1. `SomeInterface d = (x, y) -> { return x.toString() + y.toString(); };`
1. 
   ```java
   SomeInterface e = (x, y) -> {
      String s = "" + x + y;
      return s.length();
   };
   ```java
1. `SomeInterface f = (x, y) -> { return (int)(Math.random()); };`
