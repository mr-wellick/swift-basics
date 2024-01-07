# Swift Basics

# Functions and Closures

- By default, functions use their parameter names as labels for their arguments.

```swift
// We can use _ to use no argument label
// Or we can write a custom argument label before the parameter name (on, for example)
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}

greet("John", on: "Wednesday")
```

- Functions can be nested and have access to variables that were declared in the outer function.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

- Use a tuple to make a compound value.

```swift
func calcStats(scores: [Int]) -> (min: Int, max: Int, sum: Int)

let stats = calcStats(scores: [5, 3, 100, 3, 9])

// Prints "120"
print(statistics.sum)
print(statistics.2)
```

- Functions are first-class types, meaning that a function can return a function.

```swift
func makeIncrementer() -> ( (Int) -> Int ) 
```

- Functions can take another function as one of its arguments.
  
```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool
```

- Functions are a special case of closures: blocks of code that can be called later. Can write a closure without a name by surrounding code with braces { }. Use `in` to seperate func prototype and body.

```swift
var numbers = [20, 19, 7, 12]

numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

- When a closure's type is already known, you can omit the type of its parameter, its return type, or both.

```swift
var numbers = [20, 19, 7, 12]

let nums = numbers.map({ number in 3 * number })
print(mappedNumbers) // Prints "[60, 57, 21, 36]"
```

 - You can refer to parameters by number instead of by name. When a closure is the only argument to a function, you can omit the parentheses entirely.

```swift
var numbers = [20, 19, 7, 12]

let sortedNums = numbers.sorted { $0 > $1 }
print(sortedNumbers) // Prints "[20, 19, 12, 7]"
```

# Objects and Classes

- Every property needs a value assigned, either in its declaration or in the initializer.

```swift
class Shape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
        self.name = name
    }

    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}

var shape = Shape("Not a circle")
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

- Use deinit to create a deinitialzer if you need to perform some cleanup before the object is deallocated.

- Subclasses include their superclass name after their class name. Methods that override the supreclasses' implementation are marked with override.

```swift
class Square: Shape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double { return  sideLength * sideLength }
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "square")
test.area()
test.simpleDescription()
```

# Structs?
- properties
- computed properties (not stored but computed)
- initialization
- methods

- creating instances (named parameters & parameter defaults)

```swift
struct Note {
    var scientificPitchNotation: string
}
```

# Protocols?

# SwiftUI: View

- VStack takes Image and Text "stacks" the Views (VStack is a View that contains Image and Text)

```swift
import SwiftUI

struct ContentView {
    var body: some View {
        // the braces following VStack(): { ... } is an embedded function (func passed as args to other "things")
        // Returns something that behaves like a View.
        // A post-processing step going on: Takes lists and packages them as a TupleView (a list of views)
        // A func that returns a TupleView
        VStack() {
            Image(sytemName: "globe")
                .imageScale(.large)
                .forgroundColor(.orange)
            Text("Hello World!")
        }
    }
}
```


