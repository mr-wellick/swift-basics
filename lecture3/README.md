# Model-View-View Model

- Seperation of application logic & data from the UI.

- The logic is called the model

- The UI is a "parameterizable" shell that the Model feeds and brings it to life. Think of the UI as a visual manifestation of the Model.

- SwiftUI takes care of making sure the UI gets rebuilt when a Model change affects the UI.

# Model and UI

1. Rarely, the Model could just be an @state in a View (minmal to no seperation).
2. The Model might only be accessible via a gatekeeper "View Model" class (full seperation).
3. There is a View Model class, but the Model is still directly accessible (partial seperation).

# Diagrams

<img src="./img/mvvm1.jpeg"/>

<img src="./img/mvvm2.jpeg"/>

# Structs and Classes

- Read up on computed properties.

- Initializers:
    - We get a free initializer.
    - Can have any number of initializers.

- Structs:
    - Are value type.
    - Copied when passed or assigned.
    - Copy on write (when passed around it won't make a copy until its modified).
    - Functional programming.
    - No inheritance.
    - Free init that initializes ALL vars.
    - Mutability is explicit (var vs let).
    - Everything we have seen so far is a struct (except View which is a protocol).

- Classes:
    - Are reference type (lives on the heap).
    - Passed around via pointers.
    - Automatically reference counted (garbage collected when counts goes to 0).
    - Object-oriented programming.
    - Inheritance (single).
    - Free init initializes NO vars.
    - Always mutable.
    - The ViewModel in MVVM is always a class.

# Generics

- Example of generics used with a struct:

```swift
// Element is known as a Type Parameter
struct Array<Element> {
    func append(_ element: Element) { }
}

var a = Array<Int>()
a.append(5)
a.append(84)
```

# Protocols

- A protocol is sort of a "stripped-down" struct/class. It has functions and vars but no implementation (or storage)!

- Describing behaviour:

```swift
protocol Moveable {
    func move(by: Int)
    var hasMoved: Bool { get }
    var distanceFromStart: Int { get set }
}
```

- For example, View is a protocol, so CardView must behave like a View and implement the protocol:

```swift
struct CardView: View {
    var body: some View {
        ZStack {
           Text("Memoize")
            .textCase(.uppercase)
            .font(.largeTitle)
            .fontWeight(.thin)
       }
}
```

 - Can also have protocol inheritance:

 ```swift
 protocol Vehicle: Moveable {
     var passengerCount: Int { get set }
 }

 // must implement move, hasMoved, distanceFromStart, and passengerCount
 class Car: Vehicle { }

 // or we can inherit multiple protocols this way 
 class Car: Vehicle, Impoundable, Leasable { }
 ```

- A protocol is a type and can be used in the normal places you might see a type (some restrictions) with the addition of `some` and `any`.

# Uses for protocols

- Specifying behaviour of a struct, class, or enum.

- For example, `struct CardView: View` needs to implement `var body` to participate being a View. We call this process "constrains and gains."

- Another use is turning "don't cares" (generics) into "somewhat cares:"

```swift
struct Array<Element> where Element: Equatable
```

- extensions

- some & any

# Why protocols?

- It is a way for types (structs/classes/other protocols) to say what they are capable of.

- And also for other code to demand certain behaviour of another type.

- But neither side has to reveal what sort of struct or class they are.

- A way to add functionality via extensions.

- Swift is "functional (or protocol-oriented) programming."

# Function as Types

- Can declare a variable (parameter to a func, etc...) to be of type "function:"

```swift
(Int, Int) -> Bool
(Double) -> Void
() -> Array<String>
() -> Void
```

# Closures

- So common to pass functions around that we often inline them.

- We called such an inline function a "closure."
