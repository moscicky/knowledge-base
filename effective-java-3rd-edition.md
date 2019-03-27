---
description: >-
  Quotes and notes come from Effective Java by Joshua Bloch.
  https://www.amazon.com/Effective-Java-Joshua-Bloch/dp/0134685997 there are
  however my opinions once in a while
---

# Effective Java \(3rd edition\)

## Chapter 2. Creating and destroying objects

### Enforce Singleton property with a private constructor or an enum type 

#### 1. Create Singleton Object with public static field 

```text
public class Singleton {
    public static final Singleton INSTANCE = new Singleton()
    private Singleton() {} 
    //other methods 
}
```

This ensures that only one instance of object will be created and can be accessed via `Singleton.INSTANCE`. However, private constructor can still be invoked with reflection. To get over this we can throw exception in the constructor if it's asked to create the second instance.

#### 2. Create Singleton Object with private static field and factory method

```text
public class Singleton {
    private static final Singleton INSTANCE = new Singleton()
    public static Singleton getInstance() {
        return INSTANCE 
    }
    private Singleton() {} 
    //other methods 
}
```

Factory method has that advantage that it can be accessed via method reference i.e `Singleton::getInstance`

Both approaches however can be defeated with serialization. Each time the `INSTANCE` would be serialized and deserialized new `INSTANCE` would be created. To handle such case we need to provide `readResolve()` implementation in `Singleton` class. 

```text
//inside Singleton class
readResolve() { 
    return INSTANCE
}
```

#### 3. Create Singleton Object via single element enum

Arguably the best and most concise approach \(Even tough it looks odd\). One downside is that Enums can't inherit non - Enum classes. They can implement interfaces tough.

```text
public Enum Singleton {
    INSTANCE
    //methods
}
```

### Enforce noninstantiability via private constructors

We often found ourselves creating util classes composed of only static methods. It's a good practice to make constructor of such classes private. 

```text
public class DateUtils {
    private DateUtils() {}
    public static Date get Date() {...}
}
```

### Prefer dependency injection to hardwiring resources

> Static utility classes and singletons are inappropriate for classes whose behaviour is parameterized by an underlying resource.

If your class relies on behaviour of it's resources pass them in constructor, use factory or builder. Dependency injection gives you better flexibility and testability. 

### Avoid creating unnecessary objects

When possible use static factory methods instead of constructors for instating objects. Repeatedly creating the same object could seriously harm the performance. One example could be using `String.matches(regex)` , under the hood it creates `Pattern` class instance at every evaluation. It's better to create `Pattern` instance via `Patter.compile(regex)` and cache in static field. The using it like `Pattern.matcher(string).matches()` will significantly improve the performance. Sidenote: lazy initializing `Pattern` instance is not recommended due to greater complexity. 

Beware of autoboxing! Assigning primitive types to boxed primitives repeatedly can increase the runtime significantly.

### Eliminate obsolete object references

> Whenever a class manages its own memory, the programmer  should be alert for memory leaks.

In such cases GC doesn't know which objects are no longer needed. To prevent memory leaks we can null out object references.

## Chapter 3. Methods Common to All Objects

### Obey the general contract when overriding equals

Do not override `equals` when it is not needed. \(Than object will be only equal to itself\). When each instance is inherently unique, there is no logical equality test or a super class has already overridden it appropriately.

To implement `equals` properly:

* Compare argument to this object with `==` . Return `true` if that's the case
* Check whether the argument has the correct type with `instanceof` . Return `false` otherwise. If you want to allow comparison between classes that implement the same interface, use interface here.
* Cast the argument to correct type. Safety guaranteed by `instanceof`
* Check equality for each significant class element. Use `==` for primitive types, `equals` for nested objects and `Double.compare()`  and `Float.compare()` for Doubles and Floats respectively. 
* If some fields are required to contain `null` values compare such objects with `Objects.equals(Object, Object)` to avoid `NullPointerException`

Write unit tests for your equals implementation! **Always** override `hashcode` when overriding `equals`. Do not use type other than `Object` as `equals` argument.

### Override clone judiciously

Ironically `Clonable` interface doesn't provide `clone()` method. It is assumed that classes implementing `Clonable` provide proper `public clone()` method which eventually calls `Object#clone` via `super.clone` somewhere up the chain. Remember about deep copies of mutable objects. **Overall: don't use it**.

Rather than implementing infamous `Cloneable` use **copy** **constructor** or **copy factory.** One exception to this rules are arrays. They are best copied with `clone` .



