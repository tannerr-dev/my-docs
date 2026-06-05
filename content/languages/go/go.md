
[[dev-notes]]
[go strings](go-strings.md)
[[goth (go auth)]]
[Go reading order](Go%20reading%20order.md)
[[dev/dir/go_strings]]

### Types
- `bool`: a boolean value, either `true` or `false`
- `string`: a sequence of characters
- `int`: a signed integer
- `float64`: a floating-point number
- `byte`: exactly what it sounds like: 8 bits of data
```
Go's basic types are

bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point
	 
float32 float64

complex64 complex128
```
zero values
  0 false ""

The walrus operator, `:=`, declares a new variable and assigns a value to it in one line.

### Comments
```
// This is a single line comment

/*
  This is a multi-line comment
  neither of these comments will execute
  as code
*/
```

### Two Kinds of Bugs

Generally speaking, there are two kinds of errors in programming:

1. **Compilation errors.** Occur when code is compiled. It's generally better to have compilation errors because they'll never accidentally make it into production. You can't ship a program with a compiler error because the resulting executable won't even be created.
2. **Runtime errors.** Occur when a program is running. These are generally worse because they can cause your program to crash or behave unexpectedly.

### Type Sizes

Integers, [uints](https://www.cs.utah.edu/~germain/PPS/Topics/unsigned_integer.html#:~:text=Unsigned%20Integers,negative%20(zero%20or%20positive).), [floats](https://techterms.com/definition/floatingpoint), and [complex](https://www.cloudhadoop.com/2018/12/golang-tutorials-complex-types-numbers.html#:~:text=Golang%20Complex%20Type%20Numbers,complex%20number%20is%2012.8i.) numbers all have type sizes.

- Whole Numbers (No Decimal)
	`int  int8  int16  int32  int64

- Positive Whole Numbers (No Decimal)
	"uint" stands for "unsigned integer".
	`uint uint8 uint16 uint32 uint64 uintptr

- Signed Decimal Numbers
	`float32 float64

- Imaginary Numbers (Rarely Used)
	`complex64 complex128

 Unless you have a good performance related reason, you'll typically just want to use the "default" types:

    bool
    string
    int
    uint
    byte
    rune
    float64
    complex128

Constants are declared with the const keyword. They can't use the := short declaration syntax.
Constants can be primitive types like strings, integers, booleans and floats. They can not be more complex types like slices, maps and structs

    fmt.Sprintf can be used to format strings.
    %.1f rounds a float to the tenths place, %.2f rounds to the hundredths place, etc.
    %t formats a boolean value.
    %v can be used to format any value in its default representation.
    %s can be used to format a string.
    %d can be used to format an integer.

Variables in Go are passed by value (except for a few data types we haven't covered yet). "Pass by value" means that when a variable is passed into a function, that function receives a copy of the variable. The function is unable to mutate the caller's original data.



```
	// _ "modernc.org/sqlite"
	// "github.com/mattn/go-sqlite3"
```

```go
package main
import(
	"encoding/csv"
	"os"
)
func main(){
	//read and print a csv
	file, err := os.Open("data/test.csv")
	check(err)
	defer file.Close()
	reader:= csv.NewReader(file)
	records, err := reader.ReadAll()
	check(err)
	for _, record := range records{
		fmt.Println(record[0])
	}
}
```
```csv
col1, col2, col3
1, nadia, True
2,tanner, True
```

```go
package main

import (
    "database/sql"
    "fmt"
    "log"

    _ "github.com/mattn/go-sqlite3"
)

func main() {
    // Open a connection to a SQLite database (creates if not exists)
    db, err := sql.Open("sqlite3", "./example.db")
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()

    // Create a table
    _, err = db.Exec(`CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY, 
        name TEXT, 
        email TEXT
    )`)
    if err != nil {
        log.Fatal(err)
    }

    // Insert a user
    _, err = db.Exec("INSERT INTO users (name, email) VALUES (?, ?)", 
        "John Doe", "john@example.com")
    if err != nil {
        log.Fatal(err)
    }

    // Query users
    rows, err := db.Query("SELECT id, name, email FROM users")
    if err != nil {
        log.Fatal(err)
    }
    defer rows.Close()

    // Iterate through results
    for rows.Next() {
        var id int
        var name, email string
        err = rows.Scan(&id, &name, &email)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("ID: %d, Name: %s, Email: %s\n", id, name, email)
    }
}

```


