# Java notes

:sparkles:  [Awesome Java](https://github.com/akullpp/awesome-java): a curated list of awesome Java frameworks, libraries and software, by [Andreas Kull](https://github.com/akullpp).

&nbsp;

:mag: Get the location of a class at runtime:

```java
MyClass.class.getProtectionDomain().getCodeSource().getLocation()
```

&nbsp;

One-liner to create a list initialized with some data (from Java 5 on):

```java
List<String> list = Arrays.asList("a", "b", "c");
```

&nbsp;

Use an `ImmutableMap` to translate arbitrary _strings_ to _enum_ values,
instead of using _switch/case_ or _if/else_ structures: 

```java
public enum Fruit {
   APPLE, ORANGE, BANANA, RASPBERRY
}
```

```java
import com.google.common.collect.ImmutableMap; // Google Guava
import java.util.Map;
import Fruit;
import static Fruit.*;

public class Converter
{
   private static final Map<String, Fruit> FRUIT_MAP = ImmutableMap.of
      (
         "POMME", APPLE,
         "ORANGE", ORANGE,
         "BANANE", BANANA,
         "FRAMBOISE", RASPBERRY
      );
      
   public Fruit getFruitFromFrench(final String frenchFruit)
   {
      return FRUIT_MAP.get(frenchFruit);
      // Returns null if the input is null.
      // Returns null if the input is out of the mapping.
   }
}
```
