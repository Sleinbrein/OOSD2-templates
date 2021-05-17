# OOSD2-templates
Java templates die gebruikt kunnen worden voor de examens. Vaak voorkomende code kan zo gemakkelijk worden gekopieerd.

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
    if(name.isEmpty() || name == null){
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

## 8. String & Regex

## 9. Bestandsverwerking

