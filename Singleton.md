---
title: Java - Code Collection
---  
# Singleton

Ein Singleton stellt sicher, dass genau ein Objekt einer Klasse existiert. Dieses 
Singleton ist normalerweise auch global verfügbar.  

Nachteil übermäßiger Verwendung von Singleton-Klassen:  
Es besteht die große Gefahr, durch übermäßige Verwendung von Singletons ein 
Äquivalent zu globalen Variablen zu implementieren und dann prozedural statt 
objektorientiert zu programmieren.  

**Singleton class**  
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package singleton;

/**
 *
 * @author rainer
 */
public class SingleClass {

    private static final SingleClass singelCl = new SingleClass();

   /**
     * The constructor of the class is declared PRIVATE and has no parameters.
     * This means that access from outside is not possible and object formation
     * is prevented. However, an object of the class is created as a static,
     * final field that is not visible from the outside. Access to it is
     * provided by a getter method (Factory Methode) - here getInstance() in the
     * main-methode.
     */
    private SingleClass() {
        System.out.println("Object created...");
    }

    /**
     * Returns the only object of the class.
     *
     * @return
     */
    public static SingleClass getInstance() {
        return singelCl;
    }

    /**
     * Prints out your message.
     *
     * @param msg
     */
    public void printMessage(String msg) {
        System.out.println(msg);
    }
}
```

**Class Main - main()**  

```
package singleton;

/**
 *
 * @author rainer
 */
public class Main {
    
    public static void main(String[] args) {

        /**
         * The SingleClass class is not instantiated with the NEW operator. The
         * only existing object of the class is retrieved using the getInstance
         * method.
         */
        SingleClass singleCl = SingleClass.getInstance();
        
        // Calls the public methode of the singleCl object
        singleCl.printMessage("Anyone there?");
    }
}
```
**Output**  

```
run:
Object created...
Anyone there?
BUILD SUCCESSFUL (total time: 0 seconds)

```























