![Goson](https://dl.dropboxusercontent.com/u/9534337/goson_logo.svg "Goson")

JSON in golang with ease. 

### About
Goson was created to simplify reading JSON data within Golang.
This library has been heavily inspired by [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)

### Install

```shell
go get github.com/panthesingh/goson
```

### Starting

Create a goson object from JSON data. Returns an error if the data is not valid JSON.
```go
g, err := goson.Parse(data)
```
### Data

Every `Get()` call will return another goson object. You can access the underlying data with a value function.
The default value types are `float64`, `int`, `bool`, `string`. If the key does not exist the function
will return the default zero value. To check if a key exists read the section on existence.

```go
name := g.Get("name").String()
age := g.Get("age").Int()
weight := g.Get("weight").Float()
married := g.Get("married").Bool()

```
### Chaining
Chaining is very intuitive way to quickly traverse and manipulate the data you need.

```go
g.Get("key").Get("object").Index(0).Get("item").String()
```

### Existance
To check if a value exists use a type check on the `Value()` function. This returns
the goson object's underlying value as `interface{}`.

```go
v, ok := g.Get("key").Value().(string)
if !ok {
  println("key does not exist")
}
```

### Loop
Calling `Len()` on any goson object will return `len()` on the underlying value. You can use the
`Index()` function to loop through all the values.

```go
for i := 0; i < g.Len(); i++ {
    name := g.Index(i).Get("name").String()
    age := g.Index(i).Get("age").Int()
}
```

### Printing
A very useful feature is to check the JSON structure. Printing a goson
object will display pretty printed. Likewise calling `String()` should return the same ouput as a string.

```go
v := g.Get("child")
fmt.Println(v)
```

### Example

```go
package main

import (
  "github.com/panthesingh/jason"
)

func main() {

  json := `{
    "name": "Bob",
    "age": 100,
    "cars": [
      "Honda",
      "Toyota"
    ],
    "details": {
      "weight": 160.5,
      "married": false
    }
  }`

  g, _ := goson.Parse([]byte(json))
  name := g.Get("name").String()
  age := g.Get("age").Int()
  cars := g.Get("cars")
  carOne := car.Index(0).String()
  carTwo := car.Index(1).String()
  weight := g.Get("details").Get("weight").String()

}

```

### Documentation

Documentation can be found on godoc:

https://godoc.org/github.com/panthesingh/goson

### Author

Panthe Singh, http://twitter.com/panthesingh
