# Lecture 2 Notes

- Trailing Closure Syntax. If the last argument to any function or creation thing is a function itself, we can do the following:

```swift
    // last argument is a function
    ZStack(content: {
        RoundedRectangle(cornerRadius: 12).fill(.white)
        RoundedRectangle(cornerRadius: 12)
            .strokeBorder(lineWidth: 2)
        Text("👻")
    })

    // Can omit parens only if we have a trailing closure
    ZStack {
        RoundedRectangle(cornerRadius: 12).fill(.white)
        RoundedRectangle(cornerRadius: 12)
            .strokeBorder(lineWidth: 2)
        Text("👻")
    }
```
