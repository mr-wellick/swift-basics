# Protocols

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


