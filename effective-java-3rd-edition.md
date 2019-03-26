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

