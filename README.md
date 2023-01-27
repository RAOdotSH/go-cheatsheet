# Go Lang CheatSheet

Getting Started
--------


### hello.go
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world!")
}
```
Run directly
```shell script
$ go run hello.go
Hello, world!
```

### Comments
```go
// Single line comment

/* Multi-
 line comment */
```



Go Basic types
--------

### Strings

```go
s1 := "Hello" + "World"

s2 := `A "raw" string literal
can include line breaks.`

// Outputs: 10
fmt.Println(len(s1))
```
Strings are of type `string`.


### Numbers 

```go
num := 3         // int
num := 3.        // float64
num := 3 + 4i    // complex128
```
#### Operators
```go
x := 5
x++
fmt.Println("x + 4 =", x + 4)
fmt.Println("x * 4 =", x * 4) 
```

### Booleans

```go
isTrue   := true
isFalse  := false
```

#### Operators 
```go
fmt.Println(true && true)   // true 
fmt.Println(true && false)  // false
fmt.Println(true || true)   // true
fmt.Println(true || false)  // true
fmt.Println(!true)          // false
```

### Arrays
```go
┌────┬────┬────┬────┬─────┬─────┐
| 2  | 3  | 5  | 7  | 11  | 13  |
└────┴────┴────┴────┴─────┴─────┘
  0    1    2    3     4     5
```

---

```go
primes := [...]int{2, 3, 5, 7, 11, 13}
fmt.Println(len(primes)) // => 6

// Outputs: [2 3 5 7 11 13]
fmt.Println(primes)
```
---
#### 2d array
```go
var twoDimension [2][3]int
for i := 0; i < 2; i++ {
    for j := 0; j < 3; j++ {
        twoDimension[i][j] = i + j
    }
}
// => 2d:  [[0 1 2] [1 2 3]]
fmt.Println("2d: ", twoDimension)
```



### Pointers

```go
func main () {
  // taking a normal variable
  var x int = 5748
     
  // declaration of pointer
  var p *int
     
  // initialization of pointer
  p = &x
  
  fmt.Println("Value is", p)
}
```

### Slices

```go
s := make([]string, 3)
s[0] = "a"
s[1] = "b"
s = append(s, "d")

fmt.Println(s)
```

### Constants
```go
const s string = "constant"
const Phi = 1.618
const n = 500000000
const d = 3e20 / n
fmt.Println(d)
```


### Type conversions

```go
i := 90
f := float64(i)
u := uint(i)
s := strconv.Itoa(i)

// Will be equal to the character Z
s := string(i)
```


Go Strings
--------

### Strings function
```go
package main

import (
	"fmt"
	s "strings"
)

func main() {
    /* Need to import strings as s */
	fmt.Println(s.Contains("test", "e"))

    /* Build in */
    fmt.Println(len("hello"))  // => 5
    // Outputs: 101
	fmt.Println("hello"[1])
    // Outputs: e
	fmt.Println(string("hello"[1]))

}
```



### fmt.Printf {.row-span-2 .col-span-2}
```go
package main

import (
	"fmt"
	"os"
)

type point struct {
	x, y int
}

func main() {
	p := point{1, 2}
	fmt.Printf("%v\n", p)                        // => {1 2}
	fmt.Printf("%t\n", true)                     // => TRUE
}

```

Go Flow control
--------

### Conditional

```go

a := 10

if a > 20 {
    fmt.Println(">")
} else if a < 20 {
    fmt.Println("<")
} else {
    fmt.Println("=")
}
```

### Statements in if

```go
x := "hello go!"

if count := len(x); count > 0 {
    fmt.Println("Yes")
}

```
---
```go

if _, err := doThing(); err != nil {
    fmt.Println("Uh oh")
}
```

### Switch
```go {.wrap}
x := 42.0
switch x {
case 0:
case 1, 2:
    fmt.Println("Multiple matches")
case 42:   // Don't "fall through".
    fmt.Println("reached")
case 43:
    fmt.Println("Unreached")
default:
    fmt.Println("Optional")
}
```


### For loop

```go
for i := 0; i <= 10; i++ {
  fmt.Println("i: ", i)
}
```

### For-Range loop

```go {.wrap}
nums := []int{2, 3, 4}
sum := 0
for _, num := range nums {
    sum += num
}
fmt.Println("sum:", sum)
```

### While loop

```go
i := 1
for i <= 3 {
    fmt.Println(i)
    i++
}
```

### Continue keyword
```go
for i := 0; i <= 5; i++ {
    if i % 2 == 0 {
        continue
    }
    fmt.Println(i)
}
```
### Break keyword
```go
for {
    fmt.Println("loop")
    break
}
```



Go Structs & Maps
--------

### Defining

```go
package main

import (
	"fmt"
)

type Vertex struct {
	X int
	Y int
}

func main() {
	v := Vertex{1, 2}
	v.X = 4
	fmt.Println(v.X, v.Y) // => 4 2
}
```

### Literals

```go
v := Vertex{X: 1, Y: 2}
// Field names can be omitted
v := Vertex{1, 2}
// Y is implicit
v := Vertex{X: 1}
```

You can also put field names.


### Maps
```go
m := make(map[string]int)
m["k1"] = 7
m["k2"] = 13
fmt.Println(m) // => map[k1:7 k2:13]

v1 := m["k1"]
fmt.Println(v1)     // => 7
fmt.Println(len(m)) // => 2

delete(m, "k2")
fmt.Println(m) // => map[k1:7]

_, prs := m["k2"]
fmt.Println(prs) // => false

n := map[string]int{"foo": 1, "bar": 2}
fmt.Println(n) // => map[bar:2 foo:1]
```


### Pointers to structs

```go
v := &Vertex{1, 2}
v.X = 2
```

Doing `v.X` is the same as doing `(*v).X`, when `v` is a pointer.





Go Functions
--------


### Multiple arguments
```go
func plus(a int, b int) int {
    return a + b
}
func plusPlus(a, b, c int) int {
    return a + b + c
}
fmt.Println(plus(1, 2))
fmt.Println(plusPlus(1, 2, 3))
```

### Multiple return

```go
func vals() (int, int) {
    return 3, 7
}

a, b := vals()
fmt.Println(a)    // => 3
fmt.Println(b)    // => 7
```

### Function literals

```go
r1, r2 := func() (string, string) {
    x := []string{"hello", "quickref.me"}
    return x[0], x[1]
}()

// => hello quickref.me
fmt.Println(r1, r2)
```


### init function
```go
import --> const --> var --> init()
```


Go Packages
--------


### Importing

```go
import "fmt"
import "math/rand"
```
#### Same as
```go
import (
  "fmt"        // gives fmt.Println
  "math/rand"  // gives rand.Intn
)
```

### Aliases

```go
import r "math/rand"
```
---
```go
import (
    "fmt"
    r "math/rand"
)
```
---
```go
r.Intn()
```


### Packages

```go
package main

// An internal package may be imported only by another package
// that is inside the tree rooted at the parent of the internal directory
package internal
```

### Exporting names

```go
// Begin with a capital letter
func Hello () {
  ···
}
```

Go Concurrency
--------

### Goroutines {.row-span-2}

```go
package main

import (
	"fmt"
	"time"
)

func f(from string) {
	for i := 0; i < 3; i++ {
		fmt.Println(from, ":", i)
	}
}

func main() {
	f("direct")
	go f("goroutine")

	go func(msg string) {
		fmt.Println(msg)
	}("going")

	time.Sleep(time.Second)
	fmt.Println("done")
}
```

### WaitGroup

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

func w(id int, wg *sync.WaitGroup) {
	defer wg.Done()
	fmt.Printf("%d starting\n", id)

	time.Sleep(time.Second)
	fmt.Printf("%d done\n", id)
}

func main() {
	var wg sync.WaitGroup
	for i := 1; i <= 5; i++ {
		wg.Add(1)
		go w(i, &wg)
	}
	wg.Wait()
}
```

### Buffered channels

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
ch <- 3
// fatal error:
// all goroutines are asleep - deadlock
```

--------

### A basic interface

```go
type Shape interface {
  Area() float64
  Perimeter() float64
}
```

### Struct

```go
type Rectangle struct {
  Length, Width float64
}
```

### Interface example

```go {.wrap}
func main() {
  var r Shape = Rectangle{Length: 3, Width: 4}
  fmt.Printf("Type of r: %T, Area: %v, Perimeter: %v.", r, r.Area(), r.Perimeter())
}
```

Miscellaneous
-------------

### Keywords
- break
- default
- func
- interface
- select
- case
- defer
- go
- map
- struct
- chan
- else
- goto
- package
- switch
- const
- fallthrough
- if
- range
- type
- continue
- for
- import
- return
- var

### Operators and punctuation
|   |    |     |     |      |    |     |   |   |
|---|----|-----|-----|------|----|-----|---|---|
| + | &  | +=  | &=  | &&   | == | !=  | ( | ) |
| - | \| | -=  | \|= | \|\| | <  | <=  | [ | ] |
| * | ^  | *=  | ^=  | <-   | >  | >=  | { | } |
| / | << | /=  | <<= | ++   | =  | :=  | , | ; |
| % | >> | %=  | >>= | --   | !  | ... | . | : |
|   | &^ | &^= |     |      |    |     |   |   |
