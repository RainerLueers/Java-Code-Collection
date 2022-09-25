---
title: Java - Code Collection
---  
# Iterator

Das Iterator Pattern ist ein sehr häufig verwendetes Entwurfsmuster in Java und
gehört zur Kategorie der Verhaltensmuster. Es wird verwendet, um nacheinander 
auf die Elemente eines Sammlungsobjekts (Collection) zuzugreifen, ohne dass die 
zugrunde liegende Darstellung bekannt sein muss.  

Die **Iterator Klasse** ist als **innere Klasse** in der **Collection Klasse** 
(NameCollection) enthalten und wird mittels **Factory Methode** (getIterator) 
erzeugt und zurückgegeben.

Die Iterator Klasse gestaltet sich recht einfach und stellt mindestens die beiden 
Methoden **hasNext()** und **next()** zur Verfügung.  

* **hasNext()** 
	* überprüft, ob die Sammlung noch ein weiteres Element enthält.  
* **next()** 
	* gibt das nächste Element der Sammlung zurück.

**Class NameCollection**
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package iterator;

/**
 *
 * @author rainer
 */
public class NameCollection {

    private final String[] arName;

    public NameCollection(String[] inputData) {
        // Initializes the collections data
        arName = inputData;
    }

    // Returns a new iterator object
    public Iterator getIterator() {

        Iterator mIterator = new Iterator();

        return mIterator;
    }

    // Inner class provides the Iterator
    public class Iterator {

        private int index;

        private Iterator() {
            index = 0;
        }

        public boolean hasNext() {
            return index < arName.length;
        }

        public String next() {
            // Returns the name and increments the index 
            return arName[index++];
        }
    }
}
```
**Class Iterator - main()**
```
package iterator;

/**
 *
 * @author rainer
 */
public class Iterator {

    static String[] someNames = {"Bernadette", "Rainer", "Peter", "Ruth", "Ursula", "Maria", "Anton", "Ludger", "Cornelia"};

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {

        // Creates a collection
        NameCollection sammlung = new NameCollection(someNames);

        // Creates the iterators
        NameCollection.Iterator iterator1 = sammlung.getElements();
        NameCollection.Iterator iterator2 = sammlung.getElements();

        // Displays some elements of the collection
        System.out.println("\n" + iterator1.next());
        System.out.println(iterator1.next());
        System.out.println(iterator1.next() + "\n");

        // Displays all elements
        while (iterator2.hasNext()) {
            System.out.println(iterator2.next());
        }
    }
}
```
**Output**
```
run:

Bernadette
Rainer
Peter

Bernadette
Rainer
Peter
Ruth
Ursula
Maria
Anton
Ludger
Cornelia
BUILD SUCCESSFUL (total time: 0 seconds)
```




















