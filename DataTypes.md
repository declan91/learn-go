# Default Value(Zero value)

	int 0
	string ""
	bool false
	float64 0
	pointer nil
	time.Time 0001-01-01 00:00:00 +0000 UTC
	byte 0 (uint8)
	
# Variables Declaration

declaration, use this when the initial value is unknown at the time of declaration:

	var num int

short declaration, use this when the value is known, can not be used in package scoped variable declaration, equvilent to "var num int = 1":

	num := 1

blank identifier, use to avoid un-used variable error:

	_ := num

## -- multi declaration
same type:

	var num1, num2 int
  
same type multi short declaration:

	num1, num2 := 1, 2 

different type but the same group for readibility:

	var (
		num1 int, 
		num2 int, 
		s string
	) 

objects multi declaration:

	type (
		object1 struct {
			field1 string
			field2 string
		}

		object2 struct {
			field1 string
			field2 string
		}
	)

## -- redeclaration

at least one of the variables is a new variable:

	var num1 int
	num1, num2 := 1, 2

# Variable Assignment

	https://play.golang.org/p/iH6sOTkVcyB
	
  Can only assign a value with a type to a variable with the same type:

	var num1 int
	num1 = "1" -- no, "1" is string, num1 is int.
	var t bool 
	t = 1 -- no, t is bool, 1 is int.

	var f float64
	f = num1 -- no, f is float64, num1 is int.
	num1 = f -- no, f is float64, num1 is int.

	f = 1 -- yes, 1 is treated as number.

## -- multi assignment

	var (
		num1 = 1
		num2 = 2
	)

	num1, num2 = 1, 2

# Type converstion

	https://play.golang.org/p/J4JknEmqbcf

	var num1 int
	var num2 float64

	num1 = 1
	num2 = float64(num1)

	num3 := 1
	s1 := "11"
	s1converted, _ := strconv.ParseInt(s1, 10 , 32)
	num4 := num3 + int(s1converted)

	s2 := string(num1) -- yes, ascii
	s3 := string([]byte{104, 105}) -- yes
	
	
# Pointers

a pointer stores the memory address of a value, https://play.golang.org/p/lUdlZs0OtD-

	counter := 100
	p := &counter
	v := *p

\* p can indirectly reterive and update the value of the counter

	counter++
	fmt.Println(*p) // prints 101
	
	*p = 25
	fmt.Println(counter) // prints 25

	
	fmt.Printf("type of counter: %T, address of counter: %v, value of counter: %d\n", counter, &counter, counter)
	fmt.Printf("type of p: %T, address of p: %v, value of p: %v, *p: %d\n", p, &p, p, v)
	fmt.Printf("type of v: %T, address of v: %v, value of v: %d\n", v, &v, v)


## -- declaration

example: https://play.golang.org/p/toDeNO3-zp4

	package main

	import "fmt"
	import "reflect"

	type Vector struct {
	    x   int
	    y   int
	}

	func main() {
	    v := &Vector{}
	    x := new(Vector)
	    fmt.Println(reflect.TypeOf(v))
	    fmt.Println(reflect.TypeOf(x))
	}
	
One thing to note:

	new() is the only way to get a pointer to an unnamed integer or other basic type. You can write "p := new(int)" but you can't write "p := &int{0}". Other than that, it's a matter of preference.



## -- pointer with composite types

https://play.golang.org/p/C8MjxWaDBy3

when passing a variable to a func, each time the func runs, it creates a new copy of that variable.

array:

	arrays are bare values, when assigned or passed to functions, they get copied.
	if necessary, the pointer to the array needs to be passed to the func with. try to use slice instead of pointers to arrays 

	array elements address is continuous.
	
slice: 

	slice header contains a pointer to its backing array, so there is no need to use a pointer to a slice to modify its elements.

	however when adding new elements in a different func, inside the func it only has the copy of the slice headers, it means it will only add the new headers to the local copy instead of the orginal slice. note passing slices to a func is not very common, try not to use pointers with slices.
	
	slice's address is continuous in the memory.

map:

	map value is a pointer, there is no need to use pointers on map values. it works on both updating and adding new elements.
	map' elements address cannot be found, as go runtime will change the map's address behind the scene.

struct:

	pointer to the struct needs to be passed to the func to be updated.
	struct's each field has it's own address, they are continuous.


## a bit more on make() and new()

	https://stackoverflow.com/questions/9320862/why-would-i-make-or-new
	
make function allocates and initializes an object of type slice, map, or chan only. Like new, the first argument is a type. But, it can also take a second argument, the size. Unlike new, make’s return type is the same as the type of its argument, not a pointer to it. And the allocated value is initialized (not set to zero value like in new). The reason is that slice, map and chan are data structures. They need to be initialized, otherwise they won't be usable. This is the reason new() and make() need to be different.

The following examples from Effective Go make it very clear:

	p *[]int = new([]int) // *p = nil, which makes p useless
	v []int = make([]int, 100) // creates v structure that has pointer to an array, length field, and capacity field. So, v is immediately usable


# -------------------------------------------------------------------

# An explanation of & and \* from stack overflow:

https://stackoverflow.com/questions/38172661/what-is-the-meaning-of-and-in-golang

## -- the & Operator (address-of operator)

& goes in front of a variable when you want to get that variable's memory address.
	
## -- the * Operator (indirection operator)

\* goes in front of a variable that holds a memory address and resolves it (it is therefore the counterpart to the & operator). It goes and gets the thing that the pointer was pointing at, e.g. \*myString.

	myString := "Hi"
	fmt.Println(*&myString) //prints "Hi"
	
or more usefully, something like

	myStructPointer = &myStruct
	// ...
	(*myStructPointer).someAttribute = "New Value"
	
## -- \* in front of a Type

When \* is put in front of a type, e.g. \*string, it becomes part of the type declaration, so you can say "this variable holds a pointer to a string".

So the confusing thing is that the * really gets used for 2 separate (albeit related) things. The star can be an operator or part of a type.
