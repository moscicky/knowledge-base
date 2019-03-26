# Book notes

## Software Craftsman \(PL 2015\)

You are in charge of your own career. Continuous development and willingness to learn are your tasks and should be your habit, not your employer order _62-65_

Read a lot of books. Focus on those about behaviour and classics like DDD and Design Patterns. While it may take years to gather the knowledge they contain, they will be relevant for years as opposed to books about concrete technology _66-67_

Practice makes perfect. Consider pet projects when learning new technologies and ideas like TDD. Practical application will help you master it quicker _70-73_ 

Practice pair programming. It will help you write cleaner code, improve your design process. You may also learn things that you wouldn't learn on your own _74-75_

Manage your time efficiently. Ditch long hours on youtube and social media. Always have something to read with you, read it when commuting, before sleep _75-78_

Follow Extreme Programming \(XP\) principles. TDD helps you design application structure better. Continuous integration means saving time in the future.  Pair programming gives you faster feedback than PR review. Refactoring = easier maintenance for others. _110-120_

## Effective Java 3rd edition

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
readResolve(){ 
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

