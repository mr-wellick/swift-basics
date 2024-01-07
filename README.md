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

- Properties can have getters and setters

```swift
class Tiangle: Shape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        // the new value has the implicit name: newValue
        // set(newValue: Double)
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "A triangle with \(sideLength)"
    }
}

var triangle = Triangle(sideLength: 3.1, name: "triangle")
print(tiangle.perimeter) // prints 9.3

triangle.perimeter = 9.9
print(tiangle.perimeter) // prints ~ 3.3
```

- NOTE: Find a better for willSet example and update README.md

- If you don't need to compute the property but still need to provide code that's run before and after setting a new value, use willSet and didSet.

- The code you provide is run any time the value changes outside of an initializer.

```swift
class TriangleAndSquare {
    var triangle: Triangle {
        willSet { square.sideLength = newValue.sideLength }
    }

    var square: Square {
        willSet { triangle.sideLength = newValue.sideLength }
    }

    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = Triangle(sideLength: size, name: name)
    }
}

var triangleAndSquare = TriangleAndSquare(size: 10, name: "test")

print(triangleAndSquare.square.sideLength) // prints 10
print(triangleAndSquare.triangle.sideLength) // prints 10

triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength) // prints 50
```

# Optionals

- Write `?` before operations like methods, properties, and subscripting.

```swift
let optionalSquare: Square?

if optionalSquare != nil {
    print("we have something to work with")
} else {
    print("nil")
}
```

# Enumerations and Structures

- Enumerations can have methods associated with them.

- By default, Swift assigns the raw value starting at zero and incrementing by one each time; can change this behavior by explicitly specifying values.

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
            case .ace:
                return "ace"
            case .jack:
                return "jack"
            case .queen:
                return "queen"
            case .king:
                return "king"
            default:
                return String(self.rawValue)
        }
    }
}

let ace = Rank.ace
let aceRawValue = ace.rawValue

// Use `init?(rawValue:)` to make an instance of an enumeration from a raw value.
// Returns either the enumeration case or nil.
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

- Read more about this example and update docs.

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
    case let .result(sunrise, sunset):
        print("Sunrise is at \(sunrise) and sunset is at \(sunset)")
    case let .failure(message):
        print("Failure... \(message)")
}
```

# Structs

- Structures are always copied when they're passed around in your code but classes are passed by reference.

```swift
struct Card {
    var rank: Rank
    var suit: Suit // also an enum but not shown in code above

    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}

let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

- computed properties (not stored but computed)
