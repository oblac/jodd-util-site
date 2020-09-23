# Type Conversion

When setting properties, **BeanUtil** converts the type of provided value to match the destination. For this purpose, it uses Type converter utility.

Getting properties always return an `Object`. If you need to cast it to some type, you may use `TypeConverterManager#convertType`. The following snippet shows the usage:

```java
public boolean getBoolean(Object bean, String param, boolean defaultValue) {
    Boolean booleanValue = null;
    if (bean != null) {
        Object value = BeanUtil.pojo.getProperty(bean, param);
        beanValue = TypeConverterManager.convertType(value, Boolean.class);
    } catch (Exception ex) {
        // log error
    }
    if (booleanValue == null) {
        return defaultValue;
    } else {
        return booleanValue.booleanValue();
    }
}
```

