# Swift Interview Notes
##### Table of Contents  
- [Struct vs. Class](#structvsclass)  
- [Protocols](#protocols)

<a name="protocols"></a>
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

<a name="delegates"></a>
## Delegates

<a name="generics"></a>
## Generics
Swift language provides ‘Generic’ features to write flexible and reusable functions and types. Generics are used to avoid duplication and to provide abstraction. Swift standard libraries are built with generics code. Swifts ‘Arrays’ and ‘Dictionary’ types belong to generic collections. With the help of arrays and dictionaries, the arrays are defined to hold ‘Int’ values and ‘String’ values or any other types.

### Generic Data types:

### Generic Functions:

<a name="threading"></a>
## Multi-threading/Queues

<a name="archipatterns"></a>
## Architecture Patterns

<a name="observers"></a>
## Observables/Oberservers

### Property Observers

```
 var value: Double = 0.0 {
    // right before we change the value of the property
    willSet {
        print(“Old value: \(value)”)
    }
    // is called inmediatle after we assign a 
    // value to the stored property, after the value is assigned
    didSet {
        print(“New value: \(value)”)
    }
 }
 ```

<a name="dependencymanagers"></a>
## Dependency Managers

<a name="localstorage"></a>
## Local Storage

<a name="schemes"></a>
## Schemes

<a name="testing"></a>
## Testing
### Unit Testing
### UI Testing

<a name="location"></a>
## Location

<a name="localstrings"></a>
## Localizable Strings

<a name="optionals"></a>
## Optionals
In many languages, when you encounter the absence of data, you have to deal with it by writing another path for your code. There is no indication that the data doesn’t exist so at many points in your program you have to write defensive code. This isn’t the situation in Swift, and optional types are how Apple handles the absence of data in an application.

Example:

```
var myOptional: String? //with the ? at the end this means the value could be nil

if let notNilString = myOptional {
    // here we know the value is not nil and define logic and we can use 
    // notNilString going forward or we could use myOptional! 
    // (since we know it's not nil)
} else {
    //here we know the value is nil, so can do something different 
}

// above is is better than assuming myOptional will not be nil when we want to use it
// b/c we have no check that myOptional is not nil, which could cause a crash later!
let notNilString = myOptional! 
```


<a name="datatypes"></a>
## Data Types

### Classes

### Structs

### Struct vs. Class:
Classes – reference types (create instances, when accessed pointed to memory allocation for that instance)
Structs – value type objects
- Structs are preferred for relatively small and copiable objects (copying is safer then multiple references)
- Structs are preferred to hold small amounts of data, not so much logic
- B/c Structs are value types, less worry about memory leaks, thread collision (altering same reference of an object)
- The structure does not need to inherit properties or behavior from another existing type.
- Classes allow you to do things that Structs cannot:
    * Inheritance enables one class to inherit the characteristics of another.
    * Type casting enables you to check and interpret the type of a class instance at runtime.
    * Deinitializers enable an instance of a class to free up any resources it has assigned.
    * Reference counting allows more than one reference to a class instance.

Examples of good candidates for structures include:
- The size of a geometric shape, perhaps encapsulating a width property and a height property, both of type Double.
- A way to refer to ranges within a series, perhaps encapsulating a start property and a length property, both of type Int.
- A point in a 3D coordinate system, perhaps encapsulating x, y and z properties, each of type Double.

In all other cases, define a class, and create instances of that class to be managed and passed by reference. In practice, this means that most custom data constructs should be classes, not structures.

Another explanation:

_When you make a copy of a value type, it copies all the data from the thing you are copying into the new variable. They are 2 separate things and changing one does not affect the other._

_When you make a copy of a reference type, the new variable refers to the same memory location as the thing you are copying. This means that changing one will change the other since they both refer to the same memory location._

### Tuples
Tuples are ordered sets of values for specific purposes
Example:
```
var person = ("Sasha", "Blumenfeld")
var firstName = person.0 // Sasha
var lastName = person.1 // Blumenfeld
```

OR:

```
var person = (firstName: "Sasha", lastName: "Blumenfeld")
var firstName = person.firstName // Sasha
var lastName = person.lastName // Blumenfeld
```

OR:

```
var origin = (x: 0, y: 0)
var point = origin
point.x = 3
point.y = 5
print(origin) // (0, 0)
print(point) // (3, 5)
```

### Static vs. Class vs. Final Declarations

- ```static```: in value types, structs for example, this keyword mean that a method is associated at the type level rather than an instance. In reference types, it also means that the method is associated at the type level of the class but it also doesn’t allow that this method can be overriden for a subclass.
- ```class```: is how you create class methods in objective C, and they can be overriden by a subclass.
- ```final```: it’s an alias for static in methods, but you can also use it before the declaration of a class to make it immutable.
For classes, in general always use “static” to create type methods, the only time you should use “class” keyword is if your subclass really needs to override it.

### Strong vs. Weak Properties
By default any references to an object are strong, to help combat the reference cycles that may arise, ARC also allows for “weak” references, a weak reference is one that does not keep a strong hold on the instance it refers to. And doesn’t stop ARC from disposing of it.To use it we add the weak keyword to our store property declaration interface builder outlets, are created as weak stored properties by default, this is because of view controllers maintain a reference to the outlet and the outlet maintains a reference to the view controller. All properties with weak references must be optional types and by definition must be a variable so that they can be set to nil.


<a name="errorhandling"></a>
## Error Handling

<a name="typealiases"></a>
## Type Alises

<a name="accesscontrol"></a>
## Access Control
There are 5 access levels:

- ```Open ```- Is the highest access level or the least restrictive access level. You can subclass classes marked as open.
- ```Public ```- Open and public enable code written in a source file to be used anywhere within a module as well as from another module that imports it. You can use classes marked with Public but you can’t subclass them.
- ```Internal```- Enables entities to be used within any source file from their defining module, but not in any source file outside of the module. This is the default level of access.
- ```Fileprivate``` — Allows you to restrict the use of an entity within its defining source file.
- ```Private ```- Is the most restrictive access level. This means that the use of an entity is restricted to an enclosing declaration. For example, a private stored property can only be used within its class.

Access Control is most useful in two particular cases when you are writing frameworks or writing tests.
