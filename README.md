# Golang Lessons

Collection of Golang questions I have asked on CHAT-GPT

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

# go-pg

## Cool Techniques on go-pg

go-pg is a powerful ORM library for Go that provides several interesting techniques for working with PostgreSQL databases:

- Eager loading: go-pg allows you to load related data in a single query using eager loading. This can help improve performance by reducing the number of queries needed to fetch the data.

- Composite primary keys: go-pg supports composite primary keys, which allows you to use multiple columns as the primary key for a table. This can be useful in situations where a single column primary key is not sufficient.

- Custom types: go-pg allows you to use custom types for columns in your tables. This can be useful for storing and querying data in a specific format, such as JSON or ENUM.

- Raw SQL: go-pg allows you to use raw SQL queries if you need more control over the query. This can be useful for advanced queries or situations where the ORM's query builder is not sufficient.

- Batch Insert: go-pg allows you to insert multiple records at once, this can be useful for large data sets.

- Transactions: go-pg provide support for transactions, you can use it to group multiple operations in a single transaction, so that if any of the operations fail, the entire transaction will be rolled back.

- Model Hooks: go-pg provides several hooks that you can use to perform custom logic before or after certain events like before_create, after_update, etc.

- Custom Scanner: go-pg allows you to define custom scanner for your struct fields. This can be useful for custom serialization/deserialization.

These features make go-pg a powerful and flexible ORM library for working with PostgreSQL databases in Go.

## Model Hooks Pattern

go-pg provides several model hooks that you can use to perform custom logic before or after certain events, such as creating, updating, or deleting a model. Here are a few examples of how you can use these hooks to implement interesting patterns:

- Auditing: You can use the before_create and before_update hooks to automatically record information about when a model was created or updated, and by whom.

```go
type User struct {
    ID        int
    CreatedAt time.Time
    UpdatedAt time.Time
    CreatorID int
    UpdaterID int
}

func (u *User) BeforeCreate(db orm.DB) error {
    u.CreatedAt = time.Now()
    return nil
}

func (u *User) BeforeUpdate(db orm.DB) error {
    u.UpdatedAt = time.Now()
    return nil
}
```
