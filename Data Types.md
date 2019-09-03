# Default Value(Zero value)

  int 0
  
  string ""
  
  bool false
  
  float64 0
  
  pointer nil
  
  time.Time 0001-01-01 00:00:00 +0000 UTC
  

# Variables Declaration

  var num int -- declaration, use this when the initial value is unknown at the time of declaration.
  
  num := 1 -- short declaration, use this when the value is known, can not be used in package scoped variable declaration. 
           -- equvilent to "var num int = 1"

  _ = num -- blank identifier, use to avoid un-used variable error

## multi declaration
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

## redeclaration

at least one of the variables is a new variable:

	var num1 int
	num1, num2 = 1, 2

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

## multi assignment

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
	
	
