# Best Practices

- In C++, dynamic binding happens when a virtual function is called through a reference (or a pointer) to a base class. The fact that a reference (or pointer) might refer to either a base- or a derived- class object is the key to dynamic binding. Calls to virtual functions made through a reference (or pointer) are resolved at run time: The function that is called is the one defined by the actual type of the object to which the reference (or pointer) refers.
- In other words, the interface to the derived type is the combination of both the `protected` and `public` members.
- When we want to inherit the interface of a base class, then the derivation should be `public`.
- Regardless of which actual type the object has, the compiler treats the object as if it is a base type object. Treating a derived object as if it were a base type is safe, because every derived object has a base sub-object. Also, the derived class inherits the operations of the base class, meaning that any operation that might be performed on a base object is available through the derived object as well.
- `Virtual`s are resolved at run time *only* if the call is made through a reference or pointer. Only in these cases is it possible for an object's dynamic type to be unknown until run time.

|           | Virtual | Non-virtual |
| :-------: |:-------:|:-----------:|
| object    | compile-time<br>(base type) | compile-time<br>(base type) |
| reference | run-time<br>(actual type) | compile-time<br>(base type) |
| pointer   | run-time<br>(actual type) | compile-time<br>(base type) |

- Using different default arguments in the base and derived versions of the same virtual is almost guaranteed to cause trouble.
- Even though every `C` object contains an `A` part, the constructors for `C` may not initialize the `A` part directly. Instead, class `C` initializes `B`, and the constructor for class `B` in turn initializes `A`.
- Derived classes should **respect** the initialization intent of their base classes by using constructors rather than assigning to these members in the body of the constructor.
- Classes that contain only data members of class type or built-in types other than pointers usually can use the synthesized operations.
- If the derived class defines its own assignment operator, then that operator must assign the base part explicitly.
- Each destructor does only what is necessary to clean up its own members.
- If the function is virtual and the call is through a reference or pointer, then the compiler generates code to determine which version to run based on the dynamic type of the object.
- We cannot make the operator a member of our own class. If we did, then the left-hand operand would have to be an object of our class type:
    ```
    // if operator<< is a member of Sales_item
    Sales_item item;
    item << cout;
    ```

    This usage is the opposite of the normal way we use output operators defined for other types.
    If we want to support normal usage, then the left-hand operand must be of type ostream . That means that if the operator is to be a member of any class, it must be a member of class ostream . However, that class is part of the standard library. Weand anyone else who wants to define IO operatorscan't go adding members to a class in the library. If we want to use the overloaded operators to do IO for our types, we must define them as a nonmember functions. IO operators usually read or write the nonpublic data members. As a consequence, classes often make the IO operators friends.
- xxx