---
title: Java - Code Collection
---  
# Observer

Das Beobachtermuster (Observer Pattern) definiert eine **Eins-zu-Viele-Abhängigkeit** 
zwischen Objekten, sodass, wenn ein Objekt seinen Zustand ändert, alle seine abhängigen 
Objekte automatisch benachrichtigt und aktualisiert werden. Es wird auch als 
Publish-Subscribe-Pattern bezeichnet.

Beim Beobachtermuster gibt es viele Beobachter (**Subscriber-Objekte**), die ein 
bestimmtes Subjekt (**Publisher-Objekt**) beobachten. Beobachter registrieren sich 
bei einem Subjekt, um eine Benachrichtigung zu erhalten, wenn innerhalb dieses 
Subjekts eine Änderung vorgenommen wird.

Ein Beobachterobjekt kann sich jederzeit beim Subjekt registrieren oder abmelden. 
Es hilft, die Objekte **lose gekoppelt** zu machen.

## Wann sollte das Observer Pattern verwendet werden?

Wie oben beschrieben, können wir, wenn wir ein System entwerfen, bei dem 
mehrere **Entitäten** an einer möglichen Aktualisierung eines bestimmten 
zweiten **Entitätsobjekts** interessiert sind, das Beobachtermuster verwenden.

Sobald sich der **Status des Subjekts ändert, benachrichtigt das Subjekt alle 
registrierten Beobachter**, und die Beobachter können auf den aktualisierten 
Status zugreifen und entsprechend handeln.

## Beispiel aus der realen Welt für ein  Observer Pattern

Ein reales Beispiel für ein Beobachtermuster könnte ein Notrufsystem für Feuerwehrleute
sein, die immer über den Status der zentralen Notrufannahmestelle informiert werden wollen.

Wenn also der Status in der Zentrale auf "Alarm" geändert wird, erhalten alle 
registrierten Feuerwehrmänner eine Benachrichtigung.  

Ein Feuerwehrmann kann sich jederzeit bei der Zentrale registrieren oder 
abmelden. Sobald die Person nicht mehr registriert ist, erhält sie keine 
Benachrichtigungen mehr.  

Bei der Programmierung stellt das Beobachtermuster die Grundlage für 
nachrichtenorientierte Anwendungen dar.  

Wenn eine Anwendung ihren Status aktualisiert hat, benachrichtigt sie die Abonnenten 
über Aktualisierungen.   

In ähnlicher Weise werden z.B. bei der Java Programmierung alle 
Tastatur- und Mausereignisse von den Listener-Objekten und festgelegten 
Funktionen verarbeitet. Wenn der Benutzer mit der Maus klickt, wird die Funktion, 
die das Mausklickereignis abonniert hat, mit allen Kontextdaten aufgerufen, 
die ihr als Methodenargument übergeben werden

## Das Beobachtermuster benötigt  vier Objekte.

1. **Subjekt** – Schnittstelle oder abstrakte Klasse, die die Operationen zum Anhängen 
und Trennen von Beobachtern an das Subjekt definiert.
1. **ConcreteSubject** – konkrete Subjekt Klasse. Es behält den Zustand des Objekts bei 
und benachrichtigt die angeschlossenen Beobachter, wenn eine Zustandsänderung auftritt.
1. **Observer** – Schnittstelle oder abstrakte Klasse, die die zur Benachrichtigung dieses 
Objekts zu verwendenden Operationen definiert.
1. **ConcreteObserver** – konkrete Observer-Implementierungen.

## Die Feuerwehrzentrale in Java

**Subjekt als Interface**
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package observer;

/**
 *
 * @author rainer
 */
public interface Subject {

    public void attach(Observer o);
    public void detach(Observer o);
    public void notifyUpdate(AlertText m);
}

```
**Subjekt als konkrete Klasse**
```
package observer;

import java.util.ArrayList;
import java.util.List;

/**
 *
 * @author rainer
 */
public class Publisher implements Subject {

    private List<Observer> observers = new ArrayList<>();

    @Override
    public void notifyUpdate(AlertText m) {
        for (Observer o : observers) {
            o.update(m);
        }
    }

    @Override
    public void attach(observer.Observer o) {
        observers.add(o);
    }

    @Override
    public void detach(observer.Observer o) {
        observers.remove(o);
    }
}
```
**Observer als Interface**
```
package observer;

/**
 *
 * @author rainer
 */
public interface Observer {

    public void update(AlertText m);
}
```
**Observer (1) als konkrete Klasse**
```
package observer;

/**
 *
 * @author rainer
 */
public class FireFighter0ne implements Observer {

    @Override
    public void update(AlertText t) {
        System.out.println("FireFighterOne: " + t.getAlertText());
    }
}
```
**Observer (2) als konkrete Klasse**
```
package observer;

/**
 *
 * @author rainer
 */
public class FireFighterTwo implements Observer {

    @Override
    public void update(AlertText t) {
        System.out.println("FireFighterTwo: " + t.getAlertText());
    }
}
```
**Observer (3) als konkrete Klasse**
```
package observer;

/**
 *
 * @author rainer
 */
public class FireFighterThree implements Observer {

    @Override
    public void update(AlertText t) {
        System.out.println("FireFighterThree: " + t.getAlertText());
    }
}
```
**Das Objekt für die konkrete Nachricht**  
*Class AlertText ist <a href="Immutable.html" target="_blank" rel="noopener noreferrer" >Immutable</a> und somit vor ungewollte Änderungen geschützt!*

```
package observer;

/**
 *
 * @author rainer
 */
public final class AlertText {

    private final String alertText;

    public AlertText(String m) {
        this.alertText = m;
    }

    public String getAlertText() {
        return alertText;
    }
}
```
**Class Main - main()**
```
package observer;

/**
 *
 * @author rainer
 */
public class Main {

    public static void main(String[] args) {

        // Instantiates the Firefighter objects
        FireFighter0ne fireF1 = new FireFighter0ne();
        FireFighterTwo fireF2 = new FireFighterTwo();
        FireFighterThree fireF3 = new FireFighterThree();

        // Instantiates the Publisher
        Publisher p = new Publisher();

        // Registers the 3 firefighters with the help of the publisher
        p.attach(fireF1);
        p.attach(fireF2);
        p.attach(fireF3);

        // Notifies all 3 registered firefighters
        p.notifyUpdate(new AlertText("Stand by - it's burning..."));

        // Unregisters 1 firefighter
        p.detach(fireF1);

        // Notifies all registered firefighters (only 2 at this point)
        p.notifyUpdate(new AlertText("Stump up - work done!"));
    }
}
```
**Output**
```
run:
FireFighterOne: Stand by - it's burning...
FireFighterTwo: Stand by - it's burning...
FireFighterThree: Stand by - it's burning...
FireFighterTwo: Stump up - work done!
FireFighterThree: Stump up - work done!
BUILD SUCCESSFUL (total time: 0 seconds)
```

































