# Compilation
## Basic command
Compile and run a single C++ code:
```shell=
g++ helloworld.cpp -o helloworld
./helloworld
Hello, world!
```

![[Pasted image 20260306091742.png|307]]

```shell=
g++ -o program source.cpp
# =
# g++ -c source.cpp
# g++ -o program source.o
```
Note: It can speed up compilation, since you only need to re-compile a single "part.o" then link with the rest.
## Multiple source files
There are basically three kinds of source files:
- Header files
- Source files without main function
- Source file with main function
```cpp=
// add.h
#ifndef ADD_H
#define ADD_H
int add(int a, int b);
#endif
```
Note: **Header guard** prevents functions / classes from being redefined/ redeclared.

```cpp=
//add.cpp
int add(int a, int b){
    return a+b;
}
```
Note: add.h should not be included.

```cpp=
//run_add.cpp
// #include "add.cpp"
// add.cpp should not be included, since add.o will be linked by the linker
// Otherwise, add function will be defined twice

#include "add.h"
#include<iostream>
using namespace std;

int main(){
    int a,b;
    cin>>a>>b;
    int result;
    result = add(a,b);
    cout<<result<<endl;
    return 0;
}
```
Note: 
- ```#include``` is a preprosser that simply replace the line by contents in add.h (copy and paste)
- Compilation of run_add.cpp will pass even if add is not defined. The definition of add will be linked to run_add.o from add.o by the linker.

To compile multiple files:
- Compile together： ```g++ -o run_add add.cpp run_add.cpp```
	- Cons: 
		- All the files will be recompiled including unchanged ones
		- The command will be long in large projects
- Compile separately
	- ```shell=
	  g++ -c add.cpp
	  g++ -c run_add.cpp
	  g++ -o add.o run_add.cpp
	  ```
	  - Pros: Only files changed will be recompliled
	  - Cons: You should remember the changed files (Incredible so make is invented)
- Make and CMake 
### Make and CMake
#### Make
```make``` is a useful tool to carry out compilation for multiple source files.
The essence of ```make``` is that 
- it determine which ```target``` should be build/rebuild 
- by checking the ```timestamp``` 
- according to the ```dependency graph```.
It is based on a file called ```Makefile```, which follows
```
target: dependencies
    command
```

e.g.
```Makefile=
all: run_add

run_add: run_add.o add.o
    g++ -o run_add run_add.o add.o

run_add.o: run_add.cpp
    g++ -c run_add.cpp

add.o: add.cpp
    g++ -c add.cpp

clean:
    rm -f run_add *.o
```

When you run
```shell=
make
```
in the command line (terminal), make 
- Step 1: Find the target by default (```all```)
- Step 2: check the dependencies
- Step 3: build **in recursion**

If you run
```shell=
make clean
```
executable run_add and all the object files will be deleted, with only source files remaining.
Note: ```clean``` will not be executed, since it is not in the dependency graph, i.e., it is an independent node. 

#### CMake
It is a tool that automatically generaye ```make``` rules for larger projects.
\[To be continued\]
A typical workflow:
```shell=
mkdir build
cd build
cmake ..
make
```

