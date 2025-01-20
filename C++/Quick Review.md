
## Arrays
### Declaration

```
int A[5];
```

### Initialization
```
int A[]= {1,2,3,4,5};
int B[5] = {1,2,3,4,5};
```
* If an array of some size is initialized (not completely), the non initialized elements will be initialized to zero.

### Accessing

```
//standard for loop
for(int i=0; i< 5; i++){
cout << A[i] << endl;
};

//foreach loop
for(int x:A){
cout << x << endl;
}
```

### Variable Sized Arrays

```
int n ;
cout << "Enter size";
cin >> n;
//Variable sized arrays are not initialized
int A[n];
```



## Structure
### Defining a Structure
```
struct Rectangle{
int length;
int breadth;
}
```

### Declaration
```
struct Rectangle r;
```

### Accessing
```
r.length = 5;
r.breadth = 10;
```

### Declaration along with definition

```
struct Rectangle{
int length;
int breadth;
} r1,r2,r3;
```


## Pointers

### Definition
- Pointer is an address variables.
- Its used for storing addresses.
- Its used to indirectly access data.
- Resources outside the program are accessed using pointers. 
- Pointers are used for parameter passing as well . 


### Declaration
```
int a = 10;
int *p; //declaration

p = &a; //assignment

*p // dereferencing
```


### Accessing Heap memory with pointer
new operator is used to heap memory
```
int *p;
p = new int[5];
```

### Deleting/De-allocating the memory
```
delete p; //for non arrays
delete [] p; // for arrays
```

## Pointers with structures
```
struct Rectangle r = {10,15};
struct Rectangle *p = &r;

//accessing 
p -> length = 20;
p -> breadth = 10;

//Inside heap

struct Rectangle r = {10,5};
struct Rectangle *p; 
p = new Rectangle;
p = &r;
cout << p ->length << p -> breadth << endl;

```


## Reference

* Its is a nickname or an alias given to a variable.
* It must be initialized when declared.
```
int a = 10;
int &r = a; //reference 
```


## Functions

### Definition
```
int add(int a, int b){ //protoype of a function
int c;                 //Definition of a function
c = a + b;
return c;
}

//int a, b are formal paramters
//int x,  y are actual paramters
int main(){
int x,y,z;
x = 10;
y = 5;
z = add(x,y); //invocation
}
```

### Parameter passing methods

#### Pass by value
```
int func(int x, int y)

func(a,b)
```

#### Call by Address
```
int func(int* x, int* y)

func(&a, &b);
```

#### Call by Reference
Shouldn't be used for large programs

```
int func(int &x, int &y);

func(a, b)
```

## Arrays as Parameters

Arrays can be passed only by address

```
fun(int A[], int n)

int main (){
int A[5] = {1,2,3,4,5};
fun(A,5)
}
```

How to return an array

```
int * fun(int n){
int *p;
p = new int[n];
return p;
}
```

## Structures as Parameter

```
int area( struct Rectangle r1){} //call by value

int area(struct Rectangle &r1){} //call by reference

void changeLength(struct Rectangle *p, int length){} //call by address

struct Rectangle r = {10,5};
changeLength(&r, 20);



```

When a structure is passed by value, if the structure has array data members , the array will be copied and a new copy will be created for the function.

```

struct Rectangle {
 int length;
 int breadth;
 int edges[4];
};

void changeLength(struct Rectangle *p){
 for(int i = 0 ; i < 4 ; i++){
   p -> edges[i] = i+2;
 } 
 
}

//Rectangle as a Struct member variable passed as a pointer
/*struct Rectangle r ; */
/*r.length = 10;*/
/*r.breadth = 5;*/
/*for(int i=0 ; i < 4; i++){*/
/*  r.edges[i] = i+1;*/
/*}*/
/*changeLength(&r);*/
/**/
/*for(int i=0 ; i < 4; i++){*/
/*  cout << r.edges[i] << endl;*/
/*}*/

```


## Classes and Constructors

Structure everything is public in class everything is private by default.

```
class Rectangle {
private: 
int length;
int breadth;

public: 
 Rectangle(){length=breadth=1;}
 Rectagnle(int l , int b);
int area();
int perimeter();
int getLength(){return length;};
void setLength(int l){length = l;}
~Rectangle();
}

Rectangle::Rectangle(int l, int b){
length = l;
breadth = b;
}

int Rectangle::area(){
return length * breadth;
}

int Rectangle::Permiter(){
return 2*(length + breadth)
}

Rectangle::~Rectangle(){}
``` 


## Template Classes

### Generic Classes

```
template <class T>
class Arithmetic{
private: 
T a;
T b;

public: 
Arithmetic(T a, T b);
T add();
T sub();
}

template <class T>
Arithmetic<T>::Arithmetic(T a, T b){
this -> a = a;
this -> b = b;
}

template <class T>
T Arithmetic<T>::add(){
	T c;
	c = a+b;
	return c;
}

template <class t>
T Arithmetic<T>::sub(){
T c;
c = a-b;
return c;
}


int main(){
Arithmetic<int> ar(10,5);
cout << ar.add() << endl;
}
```