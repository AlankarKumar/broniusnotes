
## Minimal Program

```
int main(){}
```

* Every C++ program has exactly one global function  main.
* The int return value is the programs return value to the sytem. 
* IF no value is returned it indicates success, A non-zero value indicates failure.

### Types , Variables and Arithmetic

* bool, char , int , double.
* The memory a type takes is implementation defined. 
* Ways of initialization
```
double d1 = 2.3
double d2 {2.3}

vector<int> v {1,2,3,4,5};

int i1 = 7.2;
int i2 {7.2};
int i3 = {7.2};
// i1 becomes 7
// error: floating-point to integer conversion
// error: floating-point to integer conversion (the = is redundant)
```

* While defining a variable we dont actually need to use the type information if it can be deduced from the initializer.
```
auto b = true;
auto ch = 'x';
auto i = 123;
auto d = 1.2;
auto z = sqrt(y);
// a bool
// a char
// an int
// a double
// z has the type of whatever sqr t(y) returns
```

### Constants

* const : "I promise not to change this value". The compiler enforces the promise made by const.
* constexpr : "to be evaluated at compile time". This is used primarily to specify constants, to be saved for performance purposes.
```
const int dmv = 17;
int var = 17;
constexpr double max1 = 1.4∗square(dmv);
constexpr double max2 = 1.4∗square(var);
const double max3 = 1.4∗square(var);
// dmv is a named constant
// var is not a constant
// OK if square(17) is a constant expression
// error : var is not a constant expression
// OK, may be evaluated at run time

double sum(const vector<double>&);
vector<double> v {1.2, 3.4, 4.5};
const double s1 = sum(v);
constexpr double s2 = sum(v);
Constants
43
// sum will not modify its argument (§2.2.5)
// v is not a constant
// OK: evaluated at run time
// error : sum(v) not constant expression
```

### Constant Expression Function ? ? ? 

### Test and Loop
While + switch

### Pointers , Arrays and Loops

In an expression, prefix unary * means "contents of".
In an expression , a prefix unary & mean "address of".

In a declaration, the unary suffix & means "reference to".
A reference is similar to a pointer , the difference being you dont need to use a prefix * to access the value referred to by the reference. 

When we dont have an object to point to we use the nullptr.
```
double* pd = nullptr;
```

It is often wise to check that a pointer argument that is supposed to point to something, actually
points to something:

```
int count_x(char∗ p, char x)
// count the number of occurrences of x in p[]
// p is assumed to point to a zero-terminated array of char (or to nothing)
{
if (p==nullptr) return 0;
int count = 0;
for (; ∗p!=0; ++p)
if (∗p==x)
++count;
return count;
}
```

Note how we can move a pointer to point to the next element of an array using ++ and that we can
leave out the initializer in a for-statement if we don’t need it.

In older code, 0 or NULL is typically used instead of nullptr (§7.2.2). However, using nullptr
eliminates potential confusion between integers (such as 0 or NULL) and pointers (such as nullptr).

### User Defined Types

#### Structures

The first step in building a new type is often to organize the elements it needs into a data structure,
a struct:
struct Vector {
int sz;
// number of elements
double∗ elem; // pointer to elements
};
This first version of Vector consists of an int and a double∗.
A variable of type Vector can be defined like this:
Vector v;
However, by itself that is not of much use because v’s elem pointer doesn’t point to anything. To be
useful, we must give v some elements to point to. For example, we can construct a Vector like this:
void vector_init(Vector& v, int s)
{
v.elem = new double[s]; // allocate an array of s doubles
v.sz = s;
}
That is, v’s elem member gets a pointer produced by the new operator and v’s size member gets the
number of elements. The & in Vector& indicates that we pass v by non-const reference (§2.2.5,
§7.7); that way, vector_init() can modify the vector passed to it.
The new operator allocates memory from an area called the free store (also known as dynamic
memory and heap; §11.2)

#### Classes

```
class Vector {
public:
Vector(int s) :elem{new double[s]}, sz{s} { }
double& operator[](int i) { return elem[i]; }
int size() { return sz; }
private:
double∗ elem; // pointer to the elements
int sz;
// the number of elements
};
49
// construct a Vector
// element access: subscripting
Given that, we can define a variable of our new type Vector:
Vector v(6);
// a Vector with 6 elements

The constructor initializes
the Vector members using a member initializer list:
:elem{new double[s]}, sz{s}

That is, we first initialize elem with a pointer to s elements of type double obtained from the free
store. Then, we initialize sz to s.


Access to elements is provided by a subscript function, called operator[]. It returns a reference
to the appropriate element (a double&).


```

##### What is a Subscript function? 

```
A **subscript function** in C++ is a function that overloads the **subscript operator (`[]`)**. It allows you to define how objects of a class respond to the use of square brackets, just like arrays. This makes custom classes behave like arrays or containers, enabling intuitive and readable access to their internal elements.

### Syntax of a Subscript Function

return_type operator[](parameter_type index);


A subscript function is declared using the keyword `operator` followed by `[]`. Here's the general form:
```

### Enumerations

```
enum class Color { red, blue, green };
enum class Traffic_light { green, yellow, red };
Color col = Color::red;
Traffic_light light = Traffic_light::red;

Note that enumerators (e.g., red) are in the scope of their enum class, so that they can be used
repeatedly in different enum classes without confusion. For example, Color::red is Color’s red
which is different from Traffic_light::red.
Enumerations are used to represent small sets of integer values. They are used to make code
more readable and less error-prone than it would have been had the symbolic (and mnemonic) enu-
merator names not been used.
```

* Plain enums? 

#### Namespace

```
namespace My_code {
class complex { /* ... */ };
complex sqrt(complex);
// ...
int main();
}
int My_code::main()
{
complex z {1,2};
auto z2 = sqrt(z);
std::cout << '{' << z2.real() << ',' << z2.imag() << "}\n";
// ...
};
int main()
{
return My_code::main();
}
```

#### Static Assert

```
static_assert(4<=sizeof(int), "integers are too small"); // check integer size
```


## Abstraction Mechanisms

#### Concrete Classes

The basic idea of a Concrete type is that they behave just like built-in-types.

To increase flexibility a concrete type can keep major parts of its representation on the free store and access them through the part stored in the class object itself. 

Functions defined inside a class are in-lined by default.

The name of a destructor is the complement operator, ˜, followed by the name of the class

#### Abstract Types

In contrast, an abstract type is a type thatcompletely insulates a user from implementation details. 
To do that, we decouple the interface from the representation and give up genuine local variables. 
Since we don’t know anything about the representation of an abstract type (not even its size), we must allocate objects on the free store and access them through references or pointers.

```
class Container {
public:
virtual double& operator[](int) = 0;
virtual int size() const = 0;
virtual ˜Container() {}
};
- **`virtual`**:
    
    - The function is declared as `virtual`, meaning it can be overridden by derived classes.
    - When a function is `virtual`, the function call is resolved at runtime using **dynamic dispatch** (polymorphism), rather than at compile time (static dispatch).
- **`int size()`**:
    
    - Declares a function named `size` that returns an `int` and takes no parameters.
- **`const`**:
    
    - Indicates that the function is a **const member function**, meaning it cannot modify the state of the class (no modification of member variables is allowed, except those marked as `mutable`).
- **`= 0`**:
    
    - Specifies that this is a **pure virtual function**.
    - A pure virtual function does not have a body in the base class and **must** be implemented by any derived class for that derived class to be instantiable.
    - The `= 0` syntax is what marks the function as "pure virtual."

```

* The word virtual mean "maybe redefined later in a class defined from this class.
* functions defined with virtual keyword are called virtual functions
* The =0 syntax means the function is pure virtual and it must be defined by class that derive from the "Container class".
* Thus, it is not possible to define an object that is just a Container; a Container can only serve as the interface to a class that implements its operator[]() and size() functions. 
* A class with a pure virtual function is called an abstract class.
* A class that provides the interface to a variety of other classes is often called a polymorphic type.
* A container that implements the functions required by the interface defined by the abstract class Container could use the concrete class Vector:

```
class Vector_container : public Container { // Vector_container implements Container
Vector v;
public:
Vector_container(int s) : v(s) { }
// Vector of s elements
˜Vector_container() {}
double& operator[](int i) { return v[i]; }
int size() const { return v.size(); }
};
```

* The Vector_container is the subclass, or the derived class. 
* The Container is the superclass or the base class. 
* This is called inheritance. 

```
This Container can be used like this:
void use(Container& c)
{
const int sz = c.size();
for (int i=0; i!=sz; ++i)
cout << c[i] << '\n';
}

For a function like use(Container&) to use a Container in complete ignorance of implementation
details, some other function will have to make an object on which it can operate. For example:
void g()
{
Vector_container vc {10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0};
use(vc);
}
Since use() doesn’t know about Vector_containers but only knows the Container interface, it will
work just as well for a different implementation of a Container.
```


#### Virtual Functions

* Container object must contain information to allow it to select the right function call at runtime. 
* The usual implementation technique is for the compiler to convert the name of a virtual function into an index into a table of pointers to functions.
* This table is called "virtual function table" or "vtbl".

![[Pasted image 20250106072408.png]]


#### Class Heirarchies

