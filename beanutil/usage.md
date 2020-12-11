# Usage

### Working with bean properties

In `BeanUtil` world, bean property is a class field with its _optional_ setter and getter \(aka accessors\) methods. When accessing properties, `BeanUtil` first tries to use accessors methods. If they don't exist, `BeanUtil` fail-backs to using the field of the same visibility. Therefore, the existence of accessors methods is not required and depends on usage, which often may be handy. `BeanUtil` is used internally inside the _Jodd_ library, so this behavior applies everywhere.

Simple bean:

```java
public class Foo {
    private String readwrite;   // with getter and setter
    private String readonly;    // with getter
    ...
}
```

Usage:

```java
Foo foo = new Foo();
BeanUtil.pojo.setProperty(foo, "readwrite", "data");
BeanUtil.pojo.getProperty(foo, "readwrite");
BeanUtil.declared.setProperty(foo, "readonly", "data");
```

Lines \#2 and \#3 show common and expected `BeanUtil` usage: setting value of read-write property through its accessors methods. Setting `readonly` property in above example is only possible with default implementation, so we use `BeanUtil.declared`. This variant first tries to use `setReadonly()` method, but since such method doesn't exist, field value is accessed directly.

### Nested properties

`BeanUtil` supports nested properties. Nested properties can be java beans, a **List**, a **Map** or an **array** element:

```java
BeanUtil.pojo.getProperty(cbean, "list[0].map[foo].foo");
BeanUtil.pojo.setProperty(cbean, "arr[4].map[elem.boo].foo", "test");
```

When accessing nested properties, `BeanUtil` access one property at time and, by default, expects that all inner properties exist i.e. are not-`null`. Above example is executed like the following pseudo-code:

```java
cbean.getList().get(0).get("foo").getFoo();
cbean.getArr()[4].get("elem.boo").setFoo("test");
```

### Forced setting of nested properties

The setting of nested properties fails if one of the inner elements is `null`. Using _forced_ feature of `BeanUtil`, such properties still may be set!

```java
BeanUtil.forced.setProperty(x, "y.foo", value);
BeanUtil.forced.setProperty(x, "yy[2].foo", "xxx");
```

If the object `x` in the above example has an uninitialized property `y`, `BeanUtil` will first create a new instance of `y` type, and set it to property `y`. Then, `foo` property of newly created object `y` will be set. In the second example, `yy` is an array. If it is uninitialized, `BeanUtil` will create a new array of length 3. Then, it will create a new instance of `yy` type that will be stored as the third element of the array. Finally, the `foo` property is set.

In forced mode, `BeanUtil` tries to instantiate all uninitialized properties needed for setting the final property. Instantiation depends on the inner property type: if it is a simple bean, the no-args constructor will be invoked. If it is a list, new `ArrayList` will be created. Similar applies to arrays and map types. Additionally, `BeanUtil` will check the length of existing initialized arrays and lists and if the current size is not enough, list or array will be expanded by adding `null` elements up to the new size.

### Generics support

When creating a new element of a list, `BeanUtil` will consider existing generics information in order to create an element of correct type.

### Silent mode \(no exceptions\)

Property setting may fail for various reasons, causing an unchecked exception `BeanUtilException` to be thrown. Sometimes this is not desired behavior. For these cases, `BeanUtil` offers _silent_ implementation that does not throw any exception at all.

### Maps and lists instead of beans

You can pass maps and list instead of beans as a root object. Just omit the bean name \(since we do not work on a bean anymore\):

```java
Properties properties = new Properties();
BeanUtil.pojo.setProperty(property, "[ldap.auth.enabled]", "true");
```

### Testing of property existence

`BeanUtil` also offers a convenient way to test if some property exists:

```java
BeanUtil.pojo.hasProperty(fb, "fooInteger")
```

