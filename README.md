# OOSD2-templates
Samenvatting Object-oriented Software Developement II (OOSDII). <br>
**OPGELET**: Niet alle leerstof staat in deze "samenvatting". <br>
`Feel free to contribute! 🤝🏻`

## 1. Overerving

## 2. Polymorfisme

## 3. Lambda expressies
### Anonieme innerklasse
Een anonieme innerklasse is een klasse die binnen een methode wordt gedeclareerd maar geen naam heeft. De syntax van een anonieme inner klasse expressie is analoog aan het aanroepen van een constructor, behalve dat deze constructor vervangen wordt door een klasse definitie binnen een code blok.
````java
HelloWorld frenchGreeting = new HelloWorld(){
    public void greetSomeone(String someone){
        System.out.println("Yooo " + someone);
    }
}
````

### Functionele interface
Een functionele interface is een interface met exact 1 abstracte methode.
```java
@FunctionalInterface
public interface MyInterface{
    // the single abstract method
    String reverse(String n);
}
```

### Lambda expressie
Lambda expressies kunnen enkel gebruikt worden om functionele interfaces te implementeren. Dit is een expressie die je zoals anonieme klassen toelaat om in een stap een functionele interface te declareren en te instantiëren.
```java
// Een lambda expressie bevat volgende onderdelen:
(parameterlijst) -> {statements}
```
```java
MyInterface ref = (str) -> {
    String result = "";
    for(int i = str.length();-1; i >= 0; i--){
        result += str.charAt(i);
    }
    return result;
}
```
### Method reference
Method referenties laten je toe om te refereren naar een bestaande methode
gebruik makende van zijn naam. Op die manier zijn methode referenties
compacte en eenvoudig leesbare lambda expressies voor methodes die al een
naam hebben.
```text
HelloWorldMethodReference::printGreeting
```
```java
public class HelloWorldMethodReference {
    @FunctionalInterface
    interface HelloWorld {
        void greetSomeone(String someone);
    }
 }
 
 public void sayHello() {
    HelloWorld dutchGreeting = HelloWorldMethodReference::printGreeting;
    dutchGreeting.greetSomeone("Pete");
 }
 
 private static void printGreeting(String name) {
    System.out.println("Hello " + name);
 }

 public static void main(String[] args) {
    HelloWorldMethodReference myApp =
    new HelloWorldMethodReference();
    myApp.sayHello();
    }
}
```



## 4. Exception handling
Een exception is een uitzonderlijke gebeurtenis, die kan optreden bij het uitvoeren van een applicatie en die de normale voortgang van de applicatie onderbreekt.
Via exception handling kan die uitzonderlijke gebeurtenis opgevangen worden. Zo programmeren we 'robuuste' applicaties.

### Exception object gooien
Gebruik het `throw` statement om een exceptie te gooien. Dit statement verwacht 1 argument: een object dat gegooid kan worden.
```java
// setter gooit IllegalArgumentException bij foutieve name input
public void setName(String name){
    if(name == null || name.isEmpty()){
        throw new IllegalArgumentException("Name can not be empty.");    
    }    
}
```

### Opvangen en afhandelen van exceptions
Een exception kan enkel afgehandeld worden indien ze optreedt binnen een `try` blok. Met `catch` vangen we de exceptie op. We maken dus gebruik van een try/catch blok.

**try block**: identificeert een blok code waarin een exception kan optreden.<br>
**catch block**: identificeert een blok code, de exception handler, die een specifieke exception kan afhandelen.<br>
**finally block**: wordt altijd uitgevoerd, ook al treedt er een onverwachte exception op.
```java
try{
    // code waarin exception kan optreden
}catch(IllegalArgumentException ie){
    // afhandelen exception    
}
```

```java
try{
    // code waarin exception kan optreden
}catch(IOException | SQLException ex){
    // afhandelen exceptions 
}
```
```java
try{
    // code waarin exception kan optreden
}catch(IllegalArgumentException ie){
    // afhandelen exception    
}catch(IOException ioe){
    // afhandelen exception    
}finally{
    // code wordt altijd uitgevoerd
}
```

### Soorten exceptions
| Exception                      | Beschrijving |
|--------------------------------|--------------|
| IllegalArgumentException       |              |
| NullPointerException           |              |
| ArrayIndexOutOfBoundsException |              |
| IOException                    |              |
| NumberFormatException          |              |

### Custom Exception klasse
Het is mogelijk om je eigen exception klassen te programmeren. Een eigen Exception klasse zal altijd erven van een bestaande Exception klasse. Het is de gewoonte om de naam van die nieuwe klasse te laten eindigen op Exception, vb: EmailException.
```java
public class EmailNotUniqueException extends Exception{
    public EmailNotUniqueException(String message){
        super(message);
    }
}
```
## 5. GUI - JavaFX

## 6. Collecties

### Collection\<E\>
Deze interface vormt de basis, de root van het collection framework. Alle onderstaande interfaces stammen af van deze interface.
````java
// Methodes collection
int size()
boolean isEmpty()
boolean add(E element)
boolean remove(Object element)
Iterator<E> iterator()

// Bulk methodes
boolean containsAll(Collection<?> c)
boolean addAll(Collection<?> c)
boolean removeAll(Collection<?> c)
boolean retainAll(Collection<?> c)
void clear()
````

### List\<E\>
+ geordende collection
+ elk element heeft een index
+ dubbels ✔️
````java
// Methodes List
E get(int index)
int indexOf(Object o)
int lastIndexOf(Object o)
E remove(int index)
E set(int index, E element)

List<E> subList(int fromIndex, int toIndex) // subList maken van list
void sort(Comparator<? super E> c)          // array sorteren
<T> T[] toArray(T[] a)                      // van een list naar een array
````
Bij List<E> kan je gebruik maken van ListIterator om over de elementen van de List te itereren.
1. Itereer in twee richtingen
2. Elementen toevoegen, verwijderen, wijzigen
```java
ListIterator<E> listIterator()
ListIterator<E> listIterator(int index)     // iterator die start op de aangegeven index
        
void add(E e)
boolean hasNext() && boolean hasPrevious()
E next() & E previous()
int nextIndex() & int previousIndex()
void remove()
void set(E e)
```

### ArrayList\<E\>
**Voorkeur**: veel opzoekingen <br>
(😀) Resizeable array implementatie <br>
(😀) Constante toegangstijd voor elk element => random access. <br>
(👿) Invoegen/verwijderen element(en) => veel verschuivingen.
```java
ArrayList(int initialCapacity)
void trimToSize()
void ensureCapacity(int minCapacity)
```

### LinkedList\<E\>
**Voorkeur**: veel invoegen/verwijderen van elementen <br>
(😀) Double-linked list (referentie naar voorganger en naar zijn opvolger) <br>
(😀) Elementen worden niet verschoven bij het toevoegen van een element(en). <br>
(😀) Referenties naar voorgangers/opvolger kunnen eenvoudig aangepast worden. <br>
(👿) Sequentiële toegang => starten vanaf eerste element (trager dan ArrayList).
```java
ArrayList(int initialCapacity)
void trimToSize()
void ensureCapacity(int minCapacity)
```

### Queue\<E\>
Een queue wordt typisch gebruikt om elementen bij te houden alvorens ze te verwerken. Een queue is een FIFO structuur. <br>
(👿) Elementen in queue zijn niet te benaderen via hun positie.

```java
// retourneer speciale waarden
boolean offer(E e)
E peek()
E poll()

// retourneer exceptions
boolean add(E e)
E element()
E remove()
```

### Deque\<E\>
(😀) Double ended queue (toevoegen/verwijderen elementen kan vooraan alsook achteraan gebeuren). <br>
(👿) Vaste grote

```java
void push(E e)
E peek()
E pop()
```

### ArrayDeque\<E\>
(😀) Double ended queue (toevoegen/verwijderen elementen kan vooraan als ook achteraan gebeuren). <br>
(😀) Variabele grote.
```java
void push(E e)
E peek()
E pop()
```

### Set\<E\>
dubbels ❌ <br>
(👿) Elementen niet toegankelijk via positie. <br>
(👿) geen index.
```java

```

### HashSet\<E\>
Een concrete implementatie van Set<E> die een hashtabel als onderliggende structuur heeft. Elementen zijn niet geordend.
Hashcode van een object wordt gebruikt als index in een tabel. <br>
(😀) Elementen enorm snel te vinden. <br>
(😀) Verwijderen/toevoegen van elementen heel performant. <br>
(👿) Itereren over elementen minder performant, random volgorde bij itereren.
```java

```

### SortedSet\<E\>
Een set met een ordening van de elementen. Natuurlijke en totale ordening mogelijk. <br>
(😀) Itereren over elementen is voorspelbaar (door de sortering) <br>
```java
E first()
E last()
SortedSet<E> subset(E fromElement, E toElement)
SortedSet<E> haedset(E toElement)
SortedSet<E> tailset(E fromElement)
```

### NavigableSet\<E\>
Een NavigableSet heeft een extra notie van nabijheid.<br>
```java
E floor(E e)
E lower(E e)
E ceiling(E e)
E higher(E e)
```


## 7. Streams
Een stream is een opeenvolging van objecten die verschillende methoden ondersteunt die kunnen worden gepiped om het gewenste resultaat te verkrijgen. Streams wijzigen de databron niet. Ook is er geen geïndexeerde toegang. <br>
Databron ➞ plaatsen van een Stream ➞ resultaat

### Stream operaties
```java
.filter()
.reduce()
.forEach()
.sorted()
// Operaties op IntStreams, LongStreams, DoubleStreams
.count()
.min()
.max()
.sum()
.average()
.range(int startIncl, int endExcl)
.rangeClosed(int startIncl, int endIncl)
// Operaties op Streams
.map()
.collect()
.findFirst()
.distinct()
.mapToDouble()
```
#### IntStream, LongStream, DoubleStream operaties
```java
int [] values = {69, 666, 420};
IntStream.of(values). // vervolledig met IntStream operatie
        
// Data terug ophalen
.getAsInt()
.getAsDouble()
.getAsBoolean()
```

#### Arrays en streams
```java
Integer[] values = {2, 9, 5, 0, 3, 7, 1, 4, 8, 6};
Arrays.stream(values). // vervolledig met Stream operatie

// Data terug ophalen
.collect(Collectors.toList())
.collect(Collectors.toMap())
.collect(Collectors.toSet())
```
#### Lists en streams
```java
Employee[] employees = {
    new Employee("Keanu", "Reeves", 6666),
    new Employee("Rick", "Astley", 5000),    
}
List<Employee> list = Arrays.asList(employees);
list.stream(). // vervolledig met Stream

// Data terug ophalen
.findFirst().get();
.forEach(System.out::println);
.reduce()
.average().getAsDouble();
...

```

## 8. Strings & Regex
### String methodes
[Java String API](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html) <br>
**String methodes**
```java
String name = "Niels";
name.length(); // 5
name.charAt(1); // "i"
name.equals("YEET"); // false
name.equalsIgnoreCase("NIELS"); // true
// kopieert  de  karakters  van  een  bepaaldeString vanaf positie start t.e.m. laatste-1, in de array naar vanaf index vanafpos
name.getChars(start, laatste, destination, vanafpos)
int compareTo()
boolean regionMatches()
boolean startsWith("string")
boolean endsWith("string")
int indexOf('a');
int lastIndexOf('a')
String substring(start)
String substring(start, eind)
String concat("string")
String replace(oldChar, newChar)
String toUpperCase()
String toLowerCase()
String trim()
char[] toCharArray
String valueOf(E)
```
### StringBuilder
StringBuilder wordt gebruikt voor zogenaamde "dynamische strings". <br>
[Java StringBuilder API](https://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html) <br>
**StringBuilder methodes**
```java
int length() // aantal karakters van StringBuilder
int capacity() // Capaciteit van StringBuilder
void setLength(int newLength) // Verhoogt/verlaagt de lengte van de StringBuilder
void ensureCapacity(int minimumCapacity) // Garandeert dat de StringBuilder een minimumcapaciteit heeft

// Methodes voor karakterbewerkingen
char charAt(int index) // returnt character op index
void setCharAt(int index, char ch) // Zet ch op index
void getChars(srcBegin, srcEnd, char[] dest, int dstBegin) // characters worden gekopieerd van deze sequentie naar de bestemmingskarakter array dst.
StringBuilder reverse() // Keert inhoud van StringBuilder om

// Append methodes, tussenvoeg- en verwijdermethodes
StringBuilder append(E) // voeg E toe aan StringBuilder
StringBuilder insert(offset, E) // voeg E toe aan StringBuilder op gegeven offset
StringBuilder delete(int start, int end) // Verwijder de characters in een substring in de StringBuilder
StringBuilder deleteCharAt(int index) // Verwijder een char op index
```

### Tokenizing Strings
1. String split methode
```java
String zin = "Wow heb je echt al tot hier gelezen?"
zin.split(" "); // ["Wow", "heb", "je", "echt", "al", "tot", "hier", "gelezen?"]
```
2. Klasse StringTokenizer
```java
String zin = "Wat een legend"
StringTokenizer tokens = new StringTokenizer(zin);
while(tokens.hasMoreTokens()){
    System.out.println(tokens.nextToken());   
}
```

### Regex
#### Reguliere expressies
| Expressie | Matches                                          |
|:---------:|--------------------------------------------------|
| \d        | elk cijfer                                       |
| \W        | elke letter, cijfer of underscore                |
| \s        | elke witruimte                                   |
| .         | elk karakter, maar geen newline                  |
| \.        | een punt                                         |
| \D        | elk niet cijfer                                  |
| \W        | elke niet-letter, niet-cijfer en geen underscore |
| \S        | elke niet wit-ruimte                             |
| [abc]     | opsomming, a of b of c                           |
| [^...]    | alles wat niet tussen de haakjes staat           |
| [A-Z]     | A t.e.m. Z                                       |
| re*       | 0 of meer                                        |
| re+       | 1 of meer                                        |
| re?       | 0 of 1                                           |
| re{n}     | precies n voorkomens                             |
| re{n,m}   | tussen n en m voorkomens                         |
| a \| b    | of => a of b                                     |
| (re)      | groeperen van reguliere expressies               |
| ^         | begin                                            |
| $         | eind                                             |

#### Stringmethodes regex
```java
String replaceAll(String regex, String replacement)
String replaceFirst(String regex, String replacement)
String[] split(String regex)
```

#### Klasse Pattern en klasse Matcher
```java
String zin = "Doneer mij een RTX 3070!"
Pattern p = Pattern.compile("[\\d]");
Matcher m = p.matcher(zin);

int count = 0;
while(m.find()){
    System.out.println("Match " + ++count);
    System.out.println(m.group());
}
```




## 9. Bestandsverwerking
Om een tekstbestand te kunnen lezen en/of schrijven moet je 3 stappen doorlopen:
1. Openen bestand om te lezen of te schrijven
2. Bewerkingen uitvoeren
3. Sluiten van het geopende bestand
### Tekstbestanden
#### Schrijven naar een tekstbestand
Schrijven naar een tekstbestand maakt gebruik van een `Formatter`
```java
// Open bestand om te schrijven
try{
    output = new Formatter(Files.newOutputStream(Paths.get("src\\tekstbestand\\clients.txt"), StandardOpenOption.APPEND));
} catch (InvalidPathException ie){
    System.err.println("Error finding file.");
    System.exit(1);
} catch (IOException ex){
    System.err.println("Error creating file.")
    System.exit(1);
}

// Schrijven naar file
try{
    output.format("%d %s %s %.2f%n", record.getAccount(), record.getFirstName(), record.getLastName(), record.getBalance());    
} catch (FormatterClosedException formatterClosedException){
    System.err.println("Error writing to file.")
}
```
#### Lezen van een tekstbestand
Lezen van een tekstbestand maakt gebruik van `Scanner`
```java
// Open bestand om te lezen
try{
    input = new Scanner(Files.newInputStream(Paths.get("src\\tekstbestand\\clients.txt")));
} catch (InvalidPathException ie){
    System.err.println("Error finding file.");
    System.exit(1);
} catch (IOException ex){
    System.err.println("Error opening file.");
    System.exit(1);
}

// Lezen van file
try{
    while(input.hasNext()){
        lijst.add(new AccountRecord(input.nextInt(), input.next(), input.nextDouble()));
    } catch (InputMismatchException elementException){
        // Indien de organisatie/type gegevens niet overeenstemmen.
        System.err.println("File improperly formed.");
        input.close();
        System.exit(1);  
    } catch (NoSuchElementException elementException){
        // Er ontbreken elementen.
        System.err.println("Element missing");
        input.close();
        System.exit(1);
    } catch (IllegalStateException stateException){
        // In geval van lezen terwijl Scanner reeds gesloten is.
        System.err.println("Error reading from file.");
        System.exit(1);
    }
}
```
### Serialisatie
#### Schrijven naar een binair bestand - serialisatie
Objecten van klassen die de interface Serializable implementeren, kunnen geserialiseerd worden via `ObjectOutputStream`
```java
// Open bestand om te schrijven
try{
    output = new ObjectOutputStream(Files.newOutputStream(Paths.get("src\\serialisatie\\accounts.ser")));
} catch (InvalidPathException ie){
    // Het opgegeven pad klopt niet.
    System.err.println("Error finding file.");
    System.exit(1);
} catch (IOException ex){
    // In geval je geen schrijfrechten hebt voor de file. De file wordt niet gevonden of kan niet gecreëerd worden.
    System.err.println("Error opening file.");
    System.exit(1);
}

// Serialiseren
try{
    output.writeObject(record); // via writeObject wordt het record geserialiseerd.
} catch (IOException ex){
    System.err.println("Error writing to file.")
}
```

#### Lezen van een binair bestand - deserialisatie
Objecten van klassen die de interface Serializable implementeren, kunnen gedeserialiseerd worden via `ObjectInputStream`
```java
// Open bestand om te lezen
try{
    input = new ObjectInputStream(Files.newInputStream(Paths.get("src\\serialisatie\\accounts.ser")));
} catch (InvalidPathException ie){
    // Het opgegeven pad klopt niet.
    System.err.println("Error finding file.");    
    System.exit(1);
} catch (IOException io){
    // De file wordt niet gevonden.
    System.err.println("Error opening file.");
    System.exit(1);
}

// Deserialiseren
try {
    while (true) {
        AccountRecordrecord = (AccountRecord) input.readObject(); // Downcasting
        lijst.add(record);
    }
} catch (EOFException e) {
    // Bij het bereiken van het einde van het bestand wordt een EOFException gegooid.
} catch (ClassNotFoundException ex) {
    // Indien iets fout loopt bij het downcasten.
    System.err.print("Ongeldige objectstream");
    System.exit(1);
} catch (IOException e) {
    // De file wordt niet gevonden.
    System.err.println("Error reading file.");
    System.exit(1);
}

return lijst;
```
