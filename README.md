# Lambda Expression Implementation Guide

## Without Generics

1. Find the functional interface that you want to reference. Here's an example of a functional interface:

   ```java
   public interface SomeInterface {
      int myMethod(int x, int y);
   
   }
   ```
   
   **NOTE:** The interface you're using can only have one abstract method. If there are more, then
   the compiler will no longer be able to infer the parameters and return type of the method
   you're trying to implement.
   
1. Use the reference type of your interface to create an object reference. This reference will contain
   your lambda expression. For this example, I'll call it `lambda`.
   
   ```java
   SomeInterface lambda;
   ```
   
1. Identify the parameters (input) and return type (output) of the method in your interface.
   
   ```java
   int myMethod(int x, int y);
   ```
   
   
   | Input | Output        |
   |-------|---------------|
   | `int x` | returns `int` |
   | `int y` |               |


1. Start building the lambda expression. The format is as follows:
   
   ```java
   ( parameters ) -> { function implementation; };
   ```
  
1. In order to build a valid lambda expression for our `SomeInterface` reference, the following must be true:
   
   1.  The lambda must take in the same parameters as the method in `SomeInterface`.
   2.  The implementation in the body of the lambda must return with the same data type as 
       the method from `SomeInterface`.
   
   Because `myMethod` takes in two integers as inputs and returns an integer, our lambda expression will do the same.
   
   ```java
   SomeInterface lambda = (x, y) -> { return x + y; }; // Returns the sum of x and y
   ```
   
   **NOTE:** The types for x and y don't need to be explicitly stated in our lambda. If the compiler has access to the
   `SomeInterface` class, then it will already know what types of variables that `myMethod` should take in as parameters.
   As long as the **number** of parameters in your lambda expression is the same as the number of parameters in `myMethod`, 
   then the compiler will treat each parameter in the lambda as if they were the same data type as the respective parameters
   in `myMethod`.
   
   ```java
   SomeInterface lambda = (int x, int y) -> { return x + y; }; // This is the same as the lambda expression above!
   ```
   
### Review

Using the `SomeInterface` functional interface, which of the following lambda expressions are valid?
For the incorrect ones, what needs to be fixed?

1. `SomeInterface a = (x, y) -> { return x * y + x + 2; };`
1. `SomeInterface b = (x) -> { return x; };`
1. `SomeInterface c = (a, b) -> { return a + b; };`
1. `SomeInterface d = (x, y) -> { return Integer.toString(x) + Integer.toString(y); };`
1. 
   ```java
   SomeInterface e = (x, y) -> {
      String s = Integer.toString(x) + Integer.toString(y);
      return s.length();
   };
   ```
1. `SomeInterface f = (x, y) -> { return (int)(Math.random()); };`

## With Generics

1. Find the functional interface that you want to reference. Here's an example of a generic functional interface:

   ```java
   public interface Predicate<T> {
      boolean test(T t);
   
   }
   ```
   
   **NOTE:** The interface you're using can only have one abstract method. If there are more, then
   the compiler will no longer be able to infer the parameters and return type of the method
   you're trying to implement.
   
1. Use the reference type of your interface to create an object reference. This reference will contain
   your lambda expression. For this new example, I'll call it `p`.
   
   ```java
   Predicate p;
   ```
   
   There's a problem here, though... the `Predicate` interface is generic! We need to add a type parameter
   to our `Predicate` reference. Let's use an `Integer` for our example.
   
   ```java
   Predicate<Integer> p;
   ```
   
   This will make a variant of the `Predicate` interface, where every `T` is replaced by our type parameter:
   
   ```java
   public interface Predicate<Integer> {
      boolean test(Integer t);
   
   }
   ```
   
   If we use `String` instead, our variant of `Predicate` will look like this:
   
   ```java
   public interface Predicate<String> {
      boolean test(String t);
   
   }
   ```
   
1. Identify the parameters (input) and return type (output) of the method in your interface.
   
   ```java
   boolean test(Integer t); // For Predicate<Integer>
   ```
   
   | Input | Output |
   |-------------|-------------------|
   | `Integer t` | returns `boolean` |
   
   
   
   ```java
   boolean test(String t); // For Predicate<String>
   ```
   
   | Input | Output |
   |-------------|-------------------|
   | `String t` | returns `boolean` |

1. Start building the lambda expression. The format is as follows:
   
   ```java
   ( parameters ) -> { function implementation; };
   ```
  
1. In order to build a valid lambda expression for our `SomeInterface` reference, the following must be true:
   
   1.  The lambda must take in the same parameters as the method in `Predicate`.
   2.  The implementation in the body of the lambda must return with the same data type as 
       the method from `Predicate`.
   
   Because `test` takes in an `Integer` and returns a `boolean`, our lambda expression will do the same.
   
   ```java
    // Checks if input integer is non-negative
   Predicate<Integer> p = (x) -> { return x >= 0; };
   
   // Checks if input string is ""
   Predicate<String> strCheck = (s) -> { return s.equals(""); }; 
   ```
   
   **NOTE:** The type for x doesn't need to be explicitly stated in our lambda. If the compiler has access to the
   `Predicate` class, then it will already know what types of variables that `test` should take in as parameters.
   As long as the **number** of parameters in your lambda expression is the same as the number of parameters in `test`, 
   then the compiler will treat each parameter in the lambda as if they were the same data type as the respective parameters
   in `test`.
   
   ```java
    // These are the same as the lambda expressions above!
   Predicate<Integer> p = (int x) -> { return x >= 0; };
   Predicate<String> strCheck = (String s) -> { return s.equals(""); };
   ```
   
   
   
### Review

Using the `Predicate<Integer>` and `Predicate<String>` functional interface, which of the following lambda expressions are valid?
For the incorrect ones, what needs to be fixed?

1. `Predicate<Integer> a = (x) -> { return x % 2 == 0; };`
1. `Predicate<Integer> b = (x) -> { return "" + x + x; };`
1. 
   ```java
   Predicate<Integer> c = (x) -> { 
      if (x > 25 || x * x < 25)
         return true;
         
      return false;
   };
   ```
1. `Predicate d = (obj) -> { return obj.toString() != null; };`
1. `Predicate<String> e = s -> return true;`
1. 
   ```java
   Predicate<String> f = (s) -> {
      
      for (int i = 0; i < s.length(); i++) {
         if (i % 5 == 0 && s.charAt(i) == 'a')   
            return true;
            
      } // for
      
      return false;
      
   };
   ```



## Testing and Using Lambdas

If we're using the `Predicate` interface, this is an example of how the abstract method could be created and called:

```java

// Checks if an input character is the character 'c'
Predicate<Character> p = c -> return c == 'c';

boolean one = p.test('c'); // p.test('c') returns true
boolean two = p.test('d'); // p.test('d') returns false

if (one) System.out.println("Test one passed!"); // passes
if (two) System.out.println("Test two passed!"); // fails

```

In this example, an object is created. This object has a reference type of `Predicate<Character>`, and the object
created by our lambda expression is an implementing class of that interface. The lambda expression determines what
the `test` method in our implementing class actually does. In order to access and use that test function, we take our
reference, `p`, and call the `test` method that it contains. As with any instance method, the arguments we use need
to match up with the parameters defined in the method, so `p.test` takes in a single character.



## Lambda Expression Code Examples

```java

public static void printMatches(String[] strings, Predicate<String> p) {

   // for each String in the input String array
   
   for (String s : strings) {
      
      // print if that String passes the test from the input Predicate
      
      if (p.test(s)) {
         System.out.println(s);
      
      } // if
   
   } // for

} // printMatches

```

```java

public static void forEach(int[] numbers, Function<Integer,Integer> f) {

   // for each int in the input int array
   
   for (int x : numbers) {
      
      // give that int a new value based on the method from the input Function
      x = f.apply(x);
   
   } // for

} // printMatches

```


