# Golang Lessons from CHAT-GPT

## Create a new type that has the same fields and method

In Go, you can create a new type that has the same fields and methods as another type by using the type keyword. This is known as type alias.

Here is an example of creating a new type that has the same fields and methods as an existing type:

```go
type Person struct {
    Name string
    Age  int
}

// Creating a new type with the same fields and methods as Person
type Employee Person

func (e *Employee) Salary() int {
    return e.Age * 1000
}

func main() {
    e := Employee{
        Name: "John",
        Age:  25,
    }
    fmt.Println(e.Name) // John
    fmt.Println(e.Age)  // 25
    fmt.Println(e.Salary()) // 25000
}
```

In this example, Employee is a new type that has the same fields and methods as the Person struct. You can create extension function (i.e. Salary()) on this new type and use it like a struct.

You can also use this technique to add methods to an existing type, which is known as "type extension".

Keep in mind that Employee and Person are two separate types even though they have the same fields and methods. You cannot use Employee where a Person is expected, and vice versa, unless you explicitly convert between them.

```
p := Person{
    Name: "John",
    Age:  25,
}

e := Employee(p) // explicit conversion from Person to Employee

fmt.Println(e.Salary()) // 25000

```

In this example, we converted p which is of type Person to e which is of type Employee. This way we can call the Salary() function on e

It's important to keep in mind that, when converting between types, the memory layout of the original type and the new type must be the same, otherwise the conversion will result in a runtime panic.



