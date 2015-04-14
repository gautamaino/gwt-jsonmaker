### Features: ###

1. Converts Java Beans into json string and vice versa. Java Beans can have objects of other beans as well.

2. Support for collections like ArrayList, HashMap, HashSet, Vectors and Arrays.

3. Easy to use. Doesn't require any change in build process.

### Getting Started: ###

#### 1. add the following line in your `[`project`]`.gwt.xml file ####
```
    <inherits name="org.jsonmaker.gwt.Gwt_jsonmaker" />
```

#### 2. Make a bean class e.g. Person ####

#### 3. Make an interface with same name as bean class and 'Jsonizer' appended to it e.g. PersonJsonizer. Make it extend the Jsonizer interface ####

#### 4.To jsonize a bean, create an instance of its Jsonizer using GWT.create() method and call asString method on it ####

#### 5. To de-jsonize a json string of a bean, use JsonizerParser.parse(jsonString). ####

Below is the example code block
The Person bean without jsonizer declaration in its body
```
// a Person bean class.
class Person{
  ...
  public String getName(){...}
  public void setName(String name){...}
  ...
  public int getAge(){...}
  public void setAge(int age){...}
}
```
and jsonizer implemented in separate java file
```
/**
 * If you want to jsonize it, you need to implement an extension of 
 * Jsonizer interface using bean name suffixed with the 'Jsonizer' keyword.
 */
public interface PersonJsonizer extends Jsonizer{}
```
**The jsonizer can alternatively be defined within Person class**
```
// a Person bean class.
class Person{
  ...
  public String getName(){...}
  public void setName(String name){...}
  ...
  public int getAge(){...}
  public void setAge(int age){...}
  public interface PersonJsonizer extends Jsonizer{}
}
```
Let the jsonizing and de-jsonizing begin
```
//Create a Person Object

Person p = new Person();
p.setName("Andres");
p.setAge(28);

//Create a PersonJsonizer instance
PersonJsonzier pj = (PersonJsonizer)GWT.create(PersonJsonizer.class);
//Jsonize
String json = pj.asString(p);

// A JSON String with Person properties
//json = '{'name':'Andres','age':28}';

// Create the Person Jsonizer
PersonJsonizer jsonizer = (PersonJsonizer)GWT.create(PersonJsonizer.class);
try{
  // Translate the JSON String to a Person bean
  Person p = (Person)JsonizerParser.parse(jsonizer, json);
}catch(JsonizerException e){
  Window.alert('JSON Translation Error!');
}
```

#### 6. There is no need to create additional Jsonizers for native supported types and their collections e.g. List of Strings can be serialized as follows ####
```
final ArrayListJsonizer aj = new ArrayListJsonizer(Defaults.STRING_JSONIZER);
List<String> list = new ArrayList<String>();
list.add("gaurav1");
list.add("gaurav2");
list.add("gaurav3");
final String listJson = aj.asString(list);
```
and can be de-sierialized as follows
```
List<String> list = (ArrayList<String>)JsonizerParser.parse(aj, listJson)
```
The native supported types are given in Defaults class of jsonmaker

'Defaults' is the class which contains jsonizers for all the natively supported types e.g. String, Date, all wrapper classes like Integer, Boolean etc.