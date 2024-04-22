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

## Data types ##

### Integer types ###
    Integer types in Go: The number represents how many bits of data does each type use. 
    uint8, uint16, uint32, uint64,
    int8, int16, int32 and int64. 
    
    uint means unsigned integer. They only contain positive numbers. 
    int means signed integer. 
    
    byte is same as uint8 and rune is same as int32.
    
    Three machine dependent integer types: uint, int and uintptr. 
    
    Better to just use int when working with integers. 

### Floating Point numbers ###
    Floating point numbers are inexact. 

    NaN - not a number - for 0/0
    positive and negative infinity also exist in GoLang. 
    
    float32 and float64
    complex64 and complex128.
    
    Better to stick with float when dealing with floating point numbers. 

### Strings ###

    String literals can be created using double quotes or back ticks - "Hello World" or `Hello World`.
    Double quoted strings cannot contain new lines and allow for special escape sequences.
    
    Strings are indexed. 
    len function to find out the length of the string. len("Hello World") returns 11 - as white space is also a character.  
    String Concatenation can be done with '+' just as addition. What to do with the plus sign is determined by the compiler depending upon the data types provided. 
    
### Boolean ###

    && - and
    || - or
    !  - not
    true
    false
    
## Variables ##

```Go
    // var x string = "Hello World" is equivalent to x := "hello world"
    // No need to specify the type sometimes as the compiler can infer the type based on the value provided.  
```
    Generally use the shorter form whenever possible. 
    
    Go is lexically scoped using blocks - The variable exists within the nearest curly braces, including any nested curly braces, but not outside of them. 
    
    For creating constants use: *const*
    
    For defining multiple variables: 
```Go
    var(
        a = 15
        b = 20
        c = 45    
    )
```
     
The := syntax is shorthand for declaring and initializing a variable, e.g. for var f string = "apple" in this case. This syntax is only available inside functions.

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

```Go
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


## Arrays in Go ##

```go

var x [5]int

```

An array is a numbered sequence of elements of a single type with a fixed length. 

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





