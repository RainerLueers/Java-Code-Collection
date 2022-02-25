---
title: Java - Code Collection
---  
# Factory

Das Factory Pattern ist eines der am häufigsten verwendeten Entwurfsmuster in Java. 
Diese Art von Entwurfsmuster gilt als Erstellungsmuster, weil es eine der besten 
Möglichkeiten zum Erstellen eines Objekts bietet.

Im Factory Pattern erstellen wir Objekte, ohne dem Client die Erstellungslogik 
offenzulegen, und verweisen auf neu erstellte Objekte unter Verwendung einer 
gemeinsamen Schnittstelle. 

## Beispiel

Wir wollen 3 verschiedene Tiere (**Klassen - Cow, Cat, Dog**) mit ihren artspezifischen 
Lauten als Eigenschaft erstellen.  ***Kuh macht muh, Hund bellt und Katze miaut...* **  

Dafür implementiert jede Tierart die gleiche Schnittstelle (**Interface Animal**) und definiert 
in sich die abstrakte Methode (**giveAloud**) zur Ausgabe seines spezifischen 
Lautes (miau, muh...).

Im nächsten Schritt wird eine Factory-Klasse (**AnimalFactory**) angelegt, in der die
angeforderten Objekte mit der **Methode getAnimal** erzeugt und dann zurückgegeben 
werden können.

Die Factory-Klasse verwendet die Klasse **AnimalFactory**, um Animal-Objekt zu 
erhalten. Dafür übergibt sie die Parameter (COW / DOG / CAT) an AnimalFactory, 
für den gerade benötigten Objekttyp.

## Vorteil
Die Verwendung ein und derselben Schnittstelle für alle erstellten Animals stellt sicher, 
dass alle Animal-Objekte die gleichen Attribute enthalten, diese aber unterschiedliche 
Werte annehmen können.  

Der Zugriff auf das jeweilige Attribut, egal um welcher Animal-Art es sich dabei handelt,
ist somit immer gleich.

**Interface Animal**
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package factory;

/**
 *
 * @author rainer
 */
public interface Animal {

    public void giveAloud();
}
```
**Class Cat**
```
package factory;

/**
 *
 * @author rainer
 */
public class Cat implements Animal{

    @Override
    public void giveAloud() {
        System.out.println("American cats meow...\nDeutsche machen miau...\n");
    }    
}
```
**Class Cow**
```
package factory;

/**
 *
 * @author rainer
 */
public class Cow implements Animal {

    @Override
    public void giveAloud() {
        System.out.println("American cows moo...\nDeutsche muhen...\n");
    }
}
```
**Class Dog**
```
package factory;

/**
 *
 * @author rainer
 */
public class Dog implements Animal {

    @Override
    public void giveAloud() {
        System.out.println("American dogs bark...\nDeutsche bellen...\n");
    }
}
```
**Class AnimalFactory**
```
package factory;

/**
 *
 * @author rainer
 */
public class AnimalFactory {

    // Gets an object of an animal class depending on the animalType parameter 
    public Animal getAnimal(String animalType) {
        
        if (animalType == null) {
            return null;
        }
        if (animalType.equalsIgnoreCase("DOG")) {
            return new Dog();

        } else if (animalType.equalsIgnoreCase("CAT")) {
            return new Cat();

        } else if (animalType.equalsIgnoreCase("Cow")) {
            return new Cow();
        }

        return null;
    }
}
```
**Class Factory - main()**
```
package factory;

/**
 *
 * @author rainer
 */
public class Factory {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {

        AnimalFactory animalFactory = new AnimalFactory();

        // Gets an object of Dog
        Animal animal1 = animalFactory.getAnimal("DOG");

        // Dog gives aloud
        animal1.giveAloud();

        // Gets an object of Cat 
        Animal animal2 = animalFactory.getAnimal("CAT");

        // Cat gives aloud
        animal2.giveAloud();

        // Gets an object of Cow   
        Animal animal3 = animalFactory.getAnimal("Cow");

        // Cow gives aloud
        animal3.giveAloud();
    }
}
```
**Output**
```
run:
American dogs bark...
Deutsche bellen...

American cats meow...
Deutsche machen miau...

American cows moo...
Deutsche muhen...

BUILD SUCCESSFUL (total time: 0 seconds)
```








































