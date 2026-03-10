Pointer is a distinguishing feature of C++. Pointers' extraordinary power results from its ability to points to any data type.
Each pointer stores the address of the data it points to. It general, the data type should be specialized.

# Typical use of pointers

## Pointers and variables
```cpp=
int a;
int *p = &a;
```
or, separately,
```cpp=
int *p;
p = &a;
```
where
- ```*``` is the dereferencing operator (address -> value)
- ```&``` is the addressing operator (value -> address)
Then, ```a``` and ```*p``` mean the same thing.
## Pointers and arrays
### Static arrays
We can use a pointer to point to an array or any of its elements.
```cpp=
int a[10];
int *p = a;
```
The name of the array is exactly the address of its first element, therefore, in general, 
- ```p+i```, ```a+i``` and ```&a[i]``` all represent the address of the element with index ```i```
- ```*(p+i)```, ```*(a+i)``` and ```a[i]``` then all represent its value.
Note that ```p``` is a variable, but ```a``` is "constant", i.e., ```p = p+2``` is legal, but ```a = a+2``` is NOT legal!
### Dynamic arrays
```cpp=
int n;
int *p = new int[n];

delete [] p;
```

## Pointers and strings
### Store a string
Strings are 1-D character array that end with ```'\0'```.
```cpp=
char str[] = "I am July";
```
can be replaced by
```cpp=
char *str = "I am July";
```

### Output a string
```cpp=
printf("%s", str);
```
It will iterately output the string content until ```'\0'``` is detected.

## Pointers and functions
Pass by pointer
- for variables
- for arrays
Return a pointer
Function pointer

## Pointers and structures
Pointers can also points to cunstomer-defined data types like structures
```cpp=
struct student{
	char name[20];
	int age;
};

student A;
student* p = &A
```
The following two methods to access the attributive of the structure are equivalent:
- ```p->age```
- ```(*p).age```

