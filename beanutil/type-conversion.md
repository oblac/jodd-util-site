# Type Conversion

When setting properties, _BeanUtil_ converts the type of provided value to match the destination. For this purpose, it uses _Jodd_s [type converter](/util/typeconverter.html) utility.

Getting properties always return an `Object`. If you need to cast it to some type, you can use `TypeConverterManager#convertType`. The following snippet \(from [Liferay](http://www.liferay.com) portal\) shows the usage:

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

