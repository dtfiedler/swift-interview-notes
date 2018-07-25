# Swift Interview Notes
## Struct vs. Class:
Classes – reference types (create instances, when accessed pointed to memory allocation for that instance)
Structs – value type objects
- Structs are preferred for relatively small and copiable objects (copying is safer then multiple references)
- Structs are preferred to hold small amounts of data, not so much logic
- B/c Structs are value types, less worry about memory leaks, thread collision (altering same reference of an object)
- The structure does not need to inherit properties or behavior from another existing type.

Examples of good candidates for structures include:
- The size of a geometric shape, perhaps encapsulating a width property and a height property, both of type Double.
- A way to refer to ranges within a series, perhaps encapsulating a start property and a length property, both of type Int.
- A point in a 3D coordinate system, perhaps encapsulating x, y and z properties, each of type Double.

In all other cases, define a class, and create instances of that class to be managed and passed by reference. In practice, this means that most custom data constructs should be classes, not structures.

## Protocols:

### Protocol Properties/Values
A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform to that protocol.

Example:
```
protocol Company {
  func buy(product: Product, money: Money)
  func sell(product: Product.Type, money: Money) -> Product?
}
```
Another example: The FullyNamed protocol requires a conforming type to provide a fully-qualified name
```
protocol FullyNamed {
    var fullName: String { get }
}
struct Person: FullyNamed {
    var fullName: String
}
let john = Person(fullName: "John Appleseed")
//john.fullName is “John Appleseed”
```
This example defines a structure called Person, which represents a specific named person. It states that it adopts the FullyNamed protocol as part of the first line of its definition.

Each instance of Person has a single stored property called fullName, which is of type String. This matches the single requirement of the FullyNamed protocol, and means that Person has correctly conformed to the protocol. (Swift reports an error at compile-time if a protocol requirement is not fulfilled.)

### Protocol Methods
Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body. 

As with type property requirements, you always prefix type method requirements with the static keyword when they’re defined in a protocol. This is true even though type method requirements are prefixed with the class or static keyword when implemented by a class:

Example: 

```
protocol RandomNumberGenerator {
    func random() -> Double
}
```

Then any class that conforms to the RandomNumberGenerator protocol must implement the 'random()' method like so:

```
class LinearCongruentialGenerator: RandomNumberGenerator {
    var lastRandom = 42.0
    let m = 139968.0
    let a = 3877.0
    let c = 29573.0
    func random() -> Double {
        lastRandom = ((lastRandom * a + c).truncatingRemainder(dividingBy:m))
        return lastRandom / m
    }
}
let generator = LinearCongruentialGenerator()
print("Here's a random number: \(generator.random())")
```

## Generics

### Generic Data types:

### Generic Functions:


