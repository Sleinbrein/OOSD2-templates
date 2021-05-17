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

## 7. Streams

## 8. String & Regex

## 9. Bestandsverwerking

