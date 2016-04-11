# Arbitrary-Precision Arithmetic

For a large amount of calculation code dealing with monetary values, precise arbitrary-precision arithmetic is required. Java supports this using the `BigDecimal` class. Below is a comparison of the treatment of `BigDecimal` in the most popular JVM-based languages.


## New Instances
### Java
  - Created using the `BigDecimal(String)` constructor.
    ```java
    BigDecimal x = new BigDecimal("0.1"); // => 2.00
    ```
  - Note that the `BigDecimal(double)` constructor may introduce imprecision.
    ``` java
    BigDecimal imprecise = new BigDecimal(0.1); // => 0.1000000000000000055511151231257827021181583404541015625  
    ```

### Scala
  - Created using the `BigDecimal(String)` constructor.
  ```scala
  val x = BigDecimal("0.1") // => 0.1
  ```

### Clojure
  - Created using a BigDecimal literal ("M" suffix).
    ```clojure
    (def x 2M) ;; => 2
    ```

## Arithmetic
### Java
  - Performed through instance methods.
    ```java
    new BigDecimal("2").plus(new BigDecimal("3")); // => 5
    new BigDecimal("2").multiply(new BigDecimal("3")); // => 6
    ```

### Clojure
  - Performed through standard algebraic functions. Note that, in Clojure, function calls are of the form `(f args...)` where `f` is the function name.
    ```clojure
    (+ 2M 3M) ;; => 5
    (* 2M 3M) ;; => 6
    ```

## Equality
### Java
  - `BigDecimal.equals` will compare **both** the value and the scale. `compareTo` must be used to for algebraic equality.
    ```java
    BigDecimal x = new BigDecimal("1.23");
    BigDecimal y = new BigDecimal("1.230");
    x.equals(x) // => true
    x.equals(y) // => false
    x.compareTo(y) == 0 // => true
    ```

### Clojure
  - The standard equality function `=` performs an algebraic comparison.
    ```clojure
    (= 1.23M 1.23M) ;; => true
    (= 1.230M 1.23M) ;; => true
    ```

## Non-Terminating Decimals

### Java
  - Operations which produce a non-terminating decimal **throw exceptions**. A `RoundingMode` and `scale` or a `MathContext` must be supplied.
    ```java
    BigDecimal x = new BigDecimal("2");
    BigDecimal y = new BigDecimal("3");
    x.divide(y) // => ArithmeticException Non-terminating decimal expansion...
    x.divide(y, 5, RoundingMode.HALF_UP) // => 0.66667
    ```

### Clojure
  - Same default behavior as Java
    ```clojure
    (/ 2M 3M) ;; => => ArithmeticException Non-terminating decimal expansion...
    ```
  - Allows setting a rounding mode and precision at a lexical scope using `with-precision`. All operations within the with-precision block will share these parameters.
    ```clojure
    (with-precision 10 RoundingMode/HALF_UP
      (/ 2M 3M)) ;; => 0.6666666667M.
    ```



```javascript var x = 5```
