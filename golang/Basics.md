# Go Basics #

go.mod file defines the modules and tracks the modules that provide those packages. 



Package
: A package is a way to group functions. Every Go program is made up of packages.

- Programs start running in pacakge main.
- By convention, the package name is the same as the last element of the import path. For instance, the "math/rand" package comprises files that begin with the statement package rand.   
- A package is generally made up of all the files in the same directory. 
- A main function is executed by default when the main package is run. 
- In Go a name is exported if it starts with a capital letter. When importing a package, you can refer only to its exported name. 

## go.sum files ##
A module may have a text file named go.sum in its root directory, alongside its go.mod file. The go.sum file contains cryptographic hashes of the module’s direct and indirect dependencies. When the go command downloads a module .mod or .zip file into the module cache, it computes a hash and checks that the hash matches the corresponding hash in the main module’s go.sum file. go.sum may be empty or absent if the module has no dependencies or if all dependencies are replaced with local directories using replace directives.

## Go code ##

Go code is grouped into packages and packages are grouped into modules. The module specifies the dependencies required to run the code, including the Go version and the set of other modules it requires. 
`go mod init example.com/greetings`
If you publish a module, this must be a path from which your module can be downloaded by Go tools. That would be your code's repository. 



There are two types of Go programs: Go executables and Go libraries. 

Executable programs can be run directly from the terminal and they end with .exe

func main() is called when a program is executed.

Go is a statically typed programming language = Variables have specific type and that type cannot be changed. 

## CLI commands in Go ##

```
go version

go init

go help

godoc fmt Println

go help

go run first.go

go mod

/* The commands with go mod are:

        download    download modules to local cache
        edit        edit go.mod from tools or scripts
        graph       print module requirement graph
        init        initialize new module in current directory
        tidy        add missing and remove unused modules
        vendor      make vendored copy of dependencies
        verify      verify dependencies have expected content
        why         explain why packages or modules are needed

*/

```
## Data types ##

### Integer types ###

- Go’s integer types are uint8, uint16, uint32, uint64, int8, int16, int32, and int64.
- 8, 16, 32, and 64 tell us how many bits each of the types use.
- In addition there are two alias types: byte -> uint8 and rune -> int32.
- There are three machine dependent integer types: unit, int and uintpcr. 

Integer types in Go: The number represents how many bits of data does each type use. 
uint8, uint16, uint32, uint64,
int8, int16, int32 and int64. 

uint means unsigned integer. They only contain positive numbers. 
int means signed integer. 

byte is same as uint8 and rune is same as int32.

Three machine dependent integer types: uint, int and uintptr. 

Better to just use int when working with integers. 

### Floating Point numbers ###
- Floating point numbers are inexact. 
- float32 and float64
- complex64 and complex128.
- In addition to floating point numbers, there are also three more types: 
    - NaN - to represent not a number
    - positive infinity
    - negative infinity
- Better to stick with float when dealing with floating point numbers. 

### Strings ###
    String
    : A string is a sequence of characters with a definite length used to represent text. Go `string`s are made up of individual bytes, usually one for each character. 

    - String literals can be created using double quotes or back ticks - "Hello World" or `Hello World`.
    - Double quoted strings cannot contain new lines and allow for special escape sequences.
    Features: 
    - Strings are indexed. 
    - len function to find out the length of the string. len("Hello World") returns 11 - as white space is also a character.  
    - String Concatenation can be done with '+' just as addition. What to do with the plus sign is determined by the compiler depending upon the data types provided. 
    
### Boolean ###
    Boolean
    : A special one-bit integer used to represent true and false. 
    && - and
    || - or
    !  - not
    true
    false
    
## Variables ##
Variable
: A variable is a storage location with a specific type and an associated name. 

Go is lexically scoped using blocks. The variable exists within the nearest curly braces or blocks. 

```Go
    // var x string = "Hello World" is equivalent to x := "hello world"
    // No need to specify the type sometimes as the compiler can infer the type based on the value provided.  
```
Generally use the shorter form whenever possible. 
    
For creating constants use: *const*
    
For defining multiple variables: 
```Go
var(
    a = 15
    b = 20
    c = 45    
)
```
The := syntax is shorthand for declaring and initializing a variable. This syntax is only available inside functions.

```go
package main
import "fmt"
func main(){
    val:= 10
    fmt.Println("The value to be printed is " + val)
}
```

```go
package main
import "fmt"
func main() {
    fmt.Print("Enter a number: ")
    var input float64 // a variable input is declared
    fmt.Scanf("%f", &input) // this places the input from terminal into the input variable in the floating point data type.
    output := input * 2
    fmt.Println(output)
}
```

## Control structures ##

### for loop ###

```go
package main
import "fmt"
func main() {
    i := 1
    for i <= 10 {
        fmt.Println(i)
        i = i + 1
    }
} 
```
Go only has for loop and no other kind of control structure. It can be used in multiple ways. 

```go
    func main() {
        for i := 1; i <= 10; i++ {
            fmt.Println(i)
            }
    }

```

Another special way of using for loop in Go: 

```go
package main
import "fmt"

func main() {
	var x [5]float64
	x[0] = 10
	x[1] = 20
	x[2] = 30
	x[3] = 40
	x[4] = 50
	var total float64 = 0
	for _, key := range x {
		// i - the current position in the array and value is the same as x[i] and range followed by the variable we want to loop over.
		total += key
	}
	fmt.Println(total)
}
```
Another way of using for loop: 
```go
for i := range 10 {
		fmt.Printf("This is Pardhu, starting on GO!!! - %[1]d \n", i)
	}
```
### if conditional statement ###

```go
    if i % 2 == 0 {
     // even
    } else {
     // odd
    }

    // To use with else if

    if i % 2 == 0 {
     // divisible by 2
    } else if i % 3 == 0 {
     // divisible by 3
    } else if i % 4 == 0 {
     // divisible by 4
    }

```

### switch statement ###

```go
    switch i {
        case 0: fmt.Println("Zero")
        case 1: fmt.Println("One")
        case 2: fmt.Println("Two")
        case 3: fmt.Println("Three")
        case 4: fmt.Println("Four")
        case 5: fmt.Println("Five")
        default: fmt.Println("Unknown Number")
    }

```
Go's switch is like the one in C, C++, Java, JavaScript, and PHP, except that Go only runs the selected case, not all the cases that follow. In effect, the break statement that is needed at the end of each case in those languages is provided automatically in Go. Another important difference is that Go's switch cases need not be constants, and the values involved need not be integers. 
> break statement is provided automatically at the end of the switch and case in Go. 

### defer statement in Go ###

`defer` statement in Go defers the execution of a function until the surrounding function returns. The deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns. 
Deferred function calls are pushed onto a stack. When a function returns, its deferred calls are executed in last-in-first-out order. 

### Struct in go ###
A struct is a collection of fields. 
- Struct fields are accessed using a dot. 
- Struct fields are accessed using a struct pointer. 
- Pointers are extremely useful when paired with structs. 

## Arrays in Go ##

```go

var x [5]int

```
Array
: An array is a numbered sequence of elements of a single type with a fixed length. 

In Go we can directly print the array. No need to iterate through the indices like java. 

```go
package main
import "fmt"
func main() {
    var x [5]int
    x[4] = 100
    fmt.Println(x)
}

// Output: [0 0 0 0 100]

```

In Go, we cannot perform division operation on dissimilar types of numbers. Either both have to be integers or floats.
If two integers are used, then the division is an integer division. If two floats are used then, the division is a floating division. 
Type conversion has to be explicit in Go under certain conditions.  

A special form of loop that can be used in GoLang: 

```go

var total float64 = 0
for i, value := range x {  
// i - the current position in the array and value is the same as x[i] and range followed by the variable we want to loop over. 
total += value
}
fmt.Println(total / float64(len(x)))

// This code gives an error because we are declaring the array index position i and are not using it. Instead we can use this: 

var total float64 = 0
for _, value := range x { // _ here means that we do not need the iterator variable. A single underscore here represents that we do not need this. 
total += value
}
fmt.Println(total / float64(len(x)))


```

One of the methods to initialize the array: 

```go
x := [5]float64{ 98, 93, 77, 82, 83 }
```

If an array is initialized vertically then the last element is also followed by a comma: 

```go
x := [5]float64{
98,
93,
77,
82,
83,
}

```

The part of the array is fixed and every time the length of the array is to be changed, the type name should be changed to achieve it. 

Go's solution to this is to use Slices. 

## Slices ##

A slice is a segment of an array. Like arrays slices are indexable and have a length. Unlike arrays, this length is allowed to change. 

```go
var x []float64 // a slice is created with a length of 0. 
```
Use the built-in make function to create a slice. 

```go
x := make([]float64, 5)
```
This creates a slice that is associated with an underlying float64 array of length 5. 

Slices are always associated with some array. Slices can never be longer than the associated array. But they can be smaller. 
The make function also allows a third parameter. 
```go
x := make([]float64, 5, 10) // 10 represents the size of the underlying array the slice is associated with. 
```

Slices can also be created using the [low:high] expression:

```go
arr := [5]float64{1,2,3,4,5}
x := arr[0:5]
```
slices can also use: 
    - arr[0:]
    - arr[:5]
    - arr[1:5]

### Slice built-in functions ###

- append: append creates a new slice by taking an existing slice (the first argument) and appending all the following arguments to it.
```go
func main() {
slice1 := []int{1,2,3}
slice2 := append(slice1, 4, 5)
fmt.Println(slice1, slice2)
}
```
  
- copy: 

```go
func main() {
    slice1 := []int{1,2,3}
    slice2 := make([]int, 2)
    copy(slice2, slice1)
    fmt.Println(slice1, slice2)
}
```
slice1 - has 3 elements
slice2 - is made with only 2 indices. 
copy function copies the content of slice1 into slice2. Since slice2 can only have two elements, only the first two elements of slice1 are copied into slice2
 
## Map ##

A Map is an unordered collection of key-value pairs. It is also known as an associative array, hash table, or dictionary. Maps are used to look up a value by its associated key. 

```go
var x map[string]int // string is the key type and int is the value type. x is a map of strings to ints. 
```
Maps can also be accessed using brackets. 
Maps have to be initialized before they are used. 

```go
x := make(map[string]int)BeforeAll
x["key"] = 10
fmt.Println(x["key"])
```
Items can be deleted from the map using the built-in delete function. 

```go
name, ok := elements["Un"] // name is the result of the lookup and ok is whether the lookup is successful or not. 
fmt.Println(name, ok)
```

Shorter way to create maps: 

```go
elements := map[string]string{
"H": "Hydrogen",
"He": "Helium",
"Li": "Lithium",
"Be": "Beryllium",
"B": "Boron",
"C": "Carbon",
"N": "Nitrogen",
"O": "Oxygen",
"F": "Fluorine",
"Ne": "Neon",
}
```
Maps can also be used to store structured information. 

## Functions in Go ##

Functions - Also called as Procedures or subroutines. 

## Notes 20240429

The Go compiler will not let you declare variables that you never use. A single underscore (_) is used to tell the compiler that we don’t need this. 

## Slice

Slice
: A slice is a segment of an array. 
- Like arrays: slices are indexable and have a length.
- Unlike arrays: The length of the slices is allowed to change. 

```go
var x []int64 // This is an example of a slice. 
```
**built-in make function** for creating slices. 
```go
x := make([]float64, 5) // This creates a slice with an underlying array of length 5. 
y := make([]float64, 5, 10) // This creates a slice of length 5 with a capacity of 10. 
```
Slices are always associated with some array and they can never be longer than the array. 

**[low:high] expression** for creation of slices.
```go
arr := [5]float64{1,2,3,4,5}
x := arr[0:5]
```
Go also provides two other built-in functions to assist with slices. 
1. append: adds elements to the end of the slice. 
    - If there is sufficient capacity in the underlying array, the element is placed after the last element in the slice and the length is incremented. However, if there is not sufficient capacity, a new array is created, all of the existing elements are copied over, the new element is added onto the end, and the new slice is returned. 
```go
package main
import "fmt"
func main(){
    slice1 := []make{1,2,3}
    slice2 := append(slice1, 4, 5)
    fmt.Println(slice1, slice2)
}
```
2. copy: it takes two arguments: dst and src -> all the elements from src are copied onto dst overwriting whatever is there. 

```go
package main
import "fmt"
func main(){
    slice1 := []int{1,2,3}
    slice2 := make([]int, 5)
    copy(slice2, slice1)
    fmt.Println(slice1, slice2)

}
```
## Maps
Maps
: A map is an unordered collection of key-value pairs. -> also called associative arrays, hash tables or dictionaries. 

`var x map[string]string`
The map type is represented by the keyword map, followed by the key type in brackets and finally the value type. 

Maps can be accessed using brackets. 
Maps have to be initialized before they can be used. 

Items can also be deleted from a map using the built in `delete` function. 

```go
delete(x, 1)
```




