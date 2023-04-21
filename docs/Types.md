# Type System

Any kind of type definition is started with `type`

### Declarations

#### A Tag

The most simple kind of type is a tag, it does not store and data and may function merely as a trait.

``type AbstractTag``

#### Type as a Type Reference

Given other existing types, a new type can refer to another type with generics or as an array

```
type str = [char]
type IntVec = Vec<int>
```

#### Enumerables

```
type Enum (
    Member1 |
    Member2 |
    Member3 (str, uint)
)
```

#### Structures

```
type Structure (
    field1 uint,
    field2 str = "default value",
    field3 AnotherType
)
```

Note on Visibility: A variable becomes private when it's starting character is `_`: `_private_variable`

#### Tuples

```
type Tuple = (uint, str, bool)
type Vec3 = [int * 3]
```

#### Generics and Recursive Storage

```
type LinkedList <Type> (
    NodeEnd |
    NodeValue (
        value Type,
        before Option< LinkedList<Type> >,
        after Option< LinkedList<Type> >
    )
)

type Result <TOk, TErr> (
    Ok(TOk) |
    Err(TErr)
)

type OnlyOk <Content> = Result <Content, ()>

type Option <C> = (Null | Has(C))
```

#### Semantic Sugar: Option Shortcut

```
    be k int? = null # This is not 'null' like in other programming languages, but an unpacked enum member.
```

### Initialization

```
be s = Structure (
    field1 = 0,
    field3 = AnotherType.new()
)

be e = Enum.Member2
   e = Enum.Member3 ("Hello", 100)
   
be s str # Declaring variable without initializing
```

### Enum Unpacking

[Rust like flow control with enum](https://doc.rust-lang.org/rust-by-example/flow_control/if_let.html) is a must have!

```
if be Enum.Member3 (string_variable, numeric_variable) = e {
    # e is Enum.Member3 and variables can be used
}

if e {
    case Enum.Member3(string_variable, numeric_variable)
        # ...

    case Enum.Member2 | Enum.Member3
        # ...
}
```

## Methods

Types are declared in one place with their data, methods do not coexist in the same declaration but are added outside. The first thing to do is to navigate into the correct scope. Static functions are declared like regular `fn`s, dynamic methods require the `self` parameter as first argument

```
Type {
    fn this_is_static {
        # This method is static and requires no arguments
    }

    fn this_is_static_2 (i uint) {
        # This method is static and requires an unsigned integer argument
    }
    
    fn this_is_dynamic (self, i uint) {
        # This method is dynamic and requires an integer argument
    }
}

be k Type
Type.this_is_static()   # static function call
k.this_is_dynamic(5)    # dynamic method call
```

### [Traits](./Traits.md)

#### Native Functions

##### Auto-Declaration

By default, declaring a type with `be v Type` requires the type to be initializied in all blocks of possible logic, however sometimes the code may be too huge and a 'default' initiailizer is wanted. The function `'be'` declared a variables in all scopes where it's not overwritten. Alternatively, following a convention you can create a 'new' method which creates a new data instance of the type.

```
type Data (
    id uint,
    name str = "",
)

Data {
    be static_id uint = 0

    fn 'be' (self) -> Type {
        ret self.new()
    }
    
    fn new () -> Type {
        static_id += 1
        
        ret Type (
            id = static_id
        )
    }
    
    fn new (value str) -> Type {
        static_id += 1
        
        ret Type (
            id = static_id
            name = value
        )
    }
}
```

##### Native Traits

Taking a look at mathematical operations, `a * b` can be interpreted as `mul(a, b) -> int`. Following the same logic, different types can implement this special (native) traits

```
# Implement Add trait with Data as right argument,
# so that we implement (Data + Data) -> Data
# Alternatively we can implement a (Data + int)
# -> int addition or other with `Data<int, int>`
#
# <right parameter, return data>

Data use Add<Data, Data> {
    fn '+' (self, Data right) -> Data {
        self.new(self.name + right.name)
    }
}
```

This is the list of mathematical traits:

```
Operator  | Function                 | Explanation
   +      | fn '+' (self, T1) -> T2  | self + T1
   +      | fn '+' (self) -> T       | + self      # Unary
   -      | fn '-' (self, T1) -> T2  | self - T1
   -      | fn '-' (self) -> T       | - self      # Unary
   *      | fn '*' (self, T1) -> T2  | self * T2
   /      | fn '/' (self, T1) -> T2  | self / T2
   %      | fn '%' (self, T1) -> T2  | self % T2
   ^      | fn '^' (self, T1) -> T2  | self ^ T2
   <<     | fn '<<' (self, T1) -> T2  | self << T2
   >>     | fn '>>' (self, T1) -> T2  | self >> T2
```

This is the list of logical traits:

```
Operator  | Function                 | Explanation
   &&     | fn '&&' (self, T1) -> T2 | self && T1
   ||     | fn '||' (self, T1) -> T2 | self || T1
   !      | fn '!' (self) -> T       | !self       # Unary
   ==     | fn '==' (self, T1) -> T2 | self == T1
   !=     | fn '!=' (self, T1) -> T2 | self != T1
   >=     | fn '>=' (self, T1) -> T2 | self >= T1
   >      | fn '>' (self, T1) -> T2  | self > T1
   <=     | fn '<=' (self, T1) -> T2 | self <= T1
   <      | fn '<' (self, T1) -> T2  | self < T1
```

This is the list of setter traits:

```
Operator  | Function                 | Explanation
   =      | fn '=' (self, T1) -> T2  | self = T1
   +=     | fn '+=' (self, T1) -> T2 | self += T1
   -=     | fn '-=' (self, T1) -> T2 | self -= T1
   *=     | fn '*=' (self, T1) -> T2 | self *= T2
   /=     | fn '/=' (self, T1) -> T2 | self /= T2
   %=     | fn '%=' (self, T1) -> T2 | self %= T2
   ^=     | fn '^=' (self, T1) -> T2 | self ^= T2
   <<=    | fn '<<=' (self, T1) -> T2| self <<= T2
   >>=    | fn '>>=' (self, T1) -> T2| self >>= T2
   &&=    | fn '&&=' (self, T1) -> T2| self &&= T1
   ||=    | fn '||=' (self, T1) -> T2| self ||= T1
   
Default Implementation for integers:

uint {
    fn '+=' (self, value uint) {
        self = self + value
    }
}
```

This is the list of special/ danger traits:

```
Operator  | Function                 | Explanation
   ?      | fn '?' (self) -> T       | self?       # Unary, from behind
   .      | fn '.' (self, str) -> T  | self.mA     # Member Access, `mA` is provided as String
```

##### Iterator Function

Inspired from JavaScript's [yield](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield)

```
fn* iterable_func() -> int {
    be i = 0
    for 4 {
        printl("calculation step")
        next i
        i += 1
    }
    ret 0
}

be iterator = iterable_func()

iterator.hasNext()  # true
# calculation step  # hasNext calculates next value to see
                    # if function returns or yields. next()
                    # simply returns the value
iterator.next()     # 0
iterator.next()     # 1
iterator.next()     # 2
iterator.hasNext()  # true
iterator.next()     # 3
iterator.hasNext()  # false
iterator.next()     # 0
```

### Generics with Traits

A function can expect a certain type or a certain trait implementation:

```
fn (val Type) ...
fn <T> (val T) ...
fn <T use Trait> (val T) ...

fn <T use
    Add<int, > +
    Mul<int, T>
> (val T) -> int {
    ret val * 2
}
```
