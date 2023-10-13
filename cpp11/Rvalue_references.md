C++11 introduces a new reference termed the rvalue reference. An rvalue reference to A is created with the syntax A&&. This enables two major features: move semantics; and perfect forwarding, the ability to pass arguments while maintaining information about them as lvalues/rvalues in a generic way.

"perfect forwarding" is a term used to describe a specific technique for forwarding function arguments to other functions or constructors while preserving their value category (lvalue or rvalue) and const-qualification. It's an important concept in C++ because it allows you to write more generic and efficient code, especially when dealing with templates and generic programming.

The primary motivation for perfect forwarding is to create functions or classes that can forward their arguments to other functions or constructors without making unnecessary copies and without losing the original type information and const-qualifications of the arguments.

Universal Reference (T&&): To enable perfect forwarding, you typically use universal references, which are declared as T&& and are introduced in C++11. Universal references can bind to both lvalues and rvalues and are used in combination with template type deduction to capture the original type and value category of the argument.

std::forward: The std::forward function template is used to forward the arguments to another function or constructor. It is often used in the implementation of functions or classes that want to achieve perfect forwarding. std::forward ensures that the argument is forwarded as either an lvalue or an rvalue based on the original argument's value category.

Example:
'''
template <typename T>
void my_forwarding_function(T&& arg) {
    some_other_function(std::forward<T>(arg));
}

int main() {
    int x = 42;
    my_forwarding_function(x);  // Argument 'x' is an lvalue, forwarded as an lvalue.
    my_forwarding_function(10); // Argument '10' is an rvalue, forwarded as an rvalue.
}
'''

auto type deduction with lvalues and rvalues:
'''
int x = 0; // `x` is an lvalue of type `int`
int& xl = x; // `xl` is an lvalue of type `int&`
int&& xr = x; // compiler error -- `x` is an lvalue
int&& xr2 = 0; // `xr2` is an lvalue of type `int&&`
auto& al = x; // `al` is an lvalue of type `int&`
auto&& al2 = x; // `al2` is an lvalue of type `int&`
auto&& ar = 0; // `ar` is an lvalue of type `int&&`
'''

Move is used to transfer resources from one object to another.
It is enabled by using rvalue references to distinguish bewteen moveable resources and non-moveable resources.
