1. Support for enums. Now they can be used directly in the beans and will seamlessly serialize and de-serialize ([Issue 12](https://code.google.com/p/gwt-jsonmaker/issues/detail?id=12))

2. It is possible now to keep jsonzer and  bean in different packages. Jsonizer needs to be made aware of the bean class location using the annotation JsonizerrBean
```
@JsonizerBean("com.jsonmaker.test.client.ResultSet")
public interface ResultSetJsonizer extends Jsonizer{}
```

The previous approach of keeping the Jsonizer and bean in the same packages doesn't need this declaration and works as it used to

The code checks for the bean in the same package as the Jsonizer first. In case, the bean class is not found in the same package, the value of JsonizerBean annotation is checked