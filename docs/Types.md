# Type System

Any kind of type definition is started with `type`

#### A Tag

The most simple kind of type is a tag, it does not store and data and may function merely as a trait.

``type AbstractTag``

#### Type as a Type Reference

Given other existing types, a new type can refer to another type with generics or as an array

``type str = char()
type IntVec = Vec<int>``
