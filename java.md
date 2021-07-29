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

public class Greengrocer
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

&nbsp;

Use an _inner class_ when testing many repetitive unit test cases:

```java
   @Test
   public void testManyCases()
   {
      class LocalTestCase {
         boolean isOrganic;
         String frenchFruit;
         Fruit expectedFruit;

         LocalTestCase(boolean o, String ff, Fruit ef) {
            isOrganic = o;
            frenchFruit = ff;
            expectedFruit = ef;
         }
      }

      List<LocalTestCase> testCaseList = Arrays.asList(
         new LocalTestCase(true, "POMME",     Fruit.APPLE),
         new LocalTestCase(true, "ORANGE",    Fruit.ORANGE),
         new LocalTestCase(true, "BANANE",    Fruit.BANANA),
         new LocalTestCase(true, "FRAMBOISE", Fruit.RASPBERRY),

         new LocalTestCase(false, "POMME",     Fruit.APPLE),
         new LocalTestCase(false, "ORANGE",    Fruit.ORANGE),
         new LocalTestCase(false, "BANANE",    Fruit.BANANA),
         new LocalTestCase(false, "FRAMBOISE", Fruit.RASPBERRY),

         new LocalTestCase(true, "APPLE",     null),
         new LocalTestCase(true, "BANANA",    null),
         new LocalTestCase(true, "RASPBERRY", null),

         new LocalTestCase(false, "APPLE",     null),
         new LocalTestCase(false, "BANANA",    null),
         new LocalTestCase(false, "RASPBERRY", null),

         new LocalTestCase(true, "pomme",       null),
         new LocalTestCase(true, "Orange",      null),
         new LocalTestCase(true, " BANANE",     null),
         new LocalTestCase(true, " FRAMBOISE ", null),

         new LocalTestCase(false, "Pomme",      null),
         new LocalTestCase(false, " ORANGE ",   null),
         new LocalTestCase(false, "banane",     null),
         new LocalTestCase(false, " FRAMBOISE", null),

         new LocalTestCase(true, "",       null),
         new LocalTestCase(true, " ",      null),
         new LocalTestCase(true, "FRAISE", null),
         new LocalTestCase(true, "P",      null),
         new LocalTestCase(true, null,     null),

         new LocalTestCase(false, "",       null),
         new LocalTestCase(false, " ",      null),
         new LocalTestCase(false, "CERISE", null),
         new LocalTestCase(false, "B",      null),
         new LocalTestCase(false, null,     null)
      );

      for (LocalTestCase testCase : testCaseList) {
         Greengrocer g = new Greengrocer(testCase.isOrganic);
         assertEquals(testCase.expectedFruit, g.getFruitFromFrench(testCase.frenchFruit));
      }
   }
```

&nbsp;

Check only one specific test then build and skip all tests:
```bash
mvn clean verify -Dtest=ClassName#methodeName
mvn install -DskipTests=true
```

&nbsp;

Get current class statically:
```java
import java.lang.invoke.MethodHandles;

...

private static final Class currentClass = MethodHandles.lookup().lookupClass();

private static final String className = currentClass.getSimpleName();

```

&nbsp;

Use `Pattern.quote` to escape text part of a regular expression:
```java
import java.util.regex.Pattern;

String[] letters = "A|B|C".split(Pattern.quote("|"));

org.junit.Assert.assertEquals(3, letters.length);
```

&nbsp;

Detect plain ASCII text:

```java
import static java.nio.charset.StandardCharsets.US_ASCII;

/**
 * Check that a byte array is plain ASCII text.
 * See {@link java.lang.String#String(byte[], Charset)} to understand how it works.
 *
 * @param b a byte array
 * @return true if b is plain ASCII text, otherwise false.
 */
private static boolean isPlainAsciiText(final byte[] b)
{
   return Arrays.equals(b, new String(b, US_ASCII).getBytes(US_ASCII));
}
```

```java
import com.google.common.base.Ascii; // from com.google.guava:guava:30.1-jre

/**
 * Check that a byte value belongs to the subset of ASCII printable characters, i.e.:
 * - LINE-FEED (10)
 * - CARRIAGE-RETURN (13)
 * - all characters from SPACE (32) to TILDE (126)
 *
 * @param b a byte
 * @return true if b belongs the subset of ASCII printable characters, otherwise false.
 */
private static boolean isByteInAsciiPrintableSubset(final byte b)
{
   return (b == Ascii.LF) || (b == Ascii.CR) || (b >= Ascii.SPACE && b < Ascii.MAX);
}
```
