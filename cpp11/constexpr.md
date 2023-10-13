Constant expressions are expressions evaluated by the compiler at compile-time. Only non-complex computations can be carried out in a constant expression. Use the constexpr specifier to indicate the variable, function, etc. is a constant expression.

```
constexpr int square(int x) {
  return x * x;
}

int square2(int x) {
  return x * x;
}

int a = square(2);  // mov DWORD PTR [rbp-4], 4

int b = square2(2); // mov edi, 2
                    // call square2(int)
                    // mov DWORD PTR [rbp-8], eax
```

constexpr values are those that the compiler can evaluate at compile-time:
```
const int x = 123;
constexpr const int& y = x; // error -- constexpr variable `y` must be initialized by a constant expression
// expression must have a constant valueC/C++(28)
// test.cpp(5, 26): attempt to access run-time storage
```

In C++, constexpr is a keyword that is used to indicate that a particular expression, function, or variable can be evaluated or computed at compile-time rather than at runtime. It is primarily used for compile-time evaluation of constants and for optimization purposes. Here are the key uses of constexpr:
1 Compile-Time Constants: You can use constexpr to define constants at compile time. For example:
constexpr int myConstant = 42;
In this case, myConstant is known at compile time and can be used in situations where a constant value is required.

2 Compile-Time Function Evaluation: You can use constexpr to declare functions that can be evaluated at compile time. This is especially useful for complex computations that can be done at compile time to improve performance. For example:
constexpr int square(int x) {
    return x * x;
}
When you call square with a constant expression as an argument, the result will be computed at compile time.

3 Constexpr Variables: In C++11 and later, you can use constexpr to declare variables, indicating that their value is known at compile time. This is useful for values that do not change during program execution and are computed at compile time. 

constexpr int arraySize = 10;
int myArray[arraySize]; // This creates an array with a size known at compile time.

4 Constexpr Constructors: You can use constexpr with constructor functions to create objects with known compile-time values.
class MyObject {
public:
    constexpr MyObject(int x) : value(x) {}
    int getValue() const { return value; }
private:
    int value;
};

constexpr MyObject obj(42);
O[O


Constant expressions with classes:
```
struct Complex {
  constexpr Complex(double r, double i) : re(r), im(i) { }
  constexpr double real() { return re; }
  constexpr double imag() { return im; }

private:
  double re;
  double im;
};

constexpr Complex I(0, 1);
```


