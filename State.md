---
title: Java - Code Collection
---  
# State

Die Hauptidee des State Pattern (Zustandsmuster) besteht darin, dem Objekt zu 
ermöglichen, sein Verhalten zu ändern, ohne seine Klasse zu ändern. Durch die 
Implementierung sollte der Code außerdem ohne viele **if/else-Anweisungen** 
sauberer bleiben.  

Stellen wir uns vor, wir haben ein Paket verschickt. Die Ist-Zustände des Pakets sind 
dann vereinfacht dargestellt folgende: 

* Paket bei Annahmestelle abgegeben
* Paket zum nächsten Auslieferungslager transportiert
* Paket in Zustellung
* Paket zugestellt

Nun wollen wir je nach Ist-Zustand den Lieferstatus anzeigen.  

Der einfachste Ansatz wäre, einige boolesche Flags hinzuzufügen und 
einfache if/else-Anweisungen innerhalb jeder unserer Methoden in der 
Klasse anzuwenden. Das wird den Code in einem einfachen Szenario auch nicht 
unübersichtlich machen.  

Wenn wir aber viele oder nachträglich hinzukommenden Zuständen 
verarbeiten wollen, wird der Code komplett unübersichtlich und kaum wartbar. 

**Interface PackageState**
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package state;

/**
 *
 * @author rainer
 */
public interface PackageState {

    /**
     *
     * @param pak
     */
    public void updateState(Package pak);
}
```
**Class HandedInState**
```
package state;

/**
 *
 * @author rainer
 */
public class HandedInState implements PackageState {

    // Singleton Pattern
    private static final HandedInState instance = new HandedInState();

    public static HandedInState instance() {
        return instance;
    }

    /**
     * State transition
     *
     * @param pak
     */
    @Override
    public void updateState(Package pak) {
        System.out.println("The package has been handed over...the next step is transport to the destination");
        pak.setCurrentState(OnTransportState.instance());
    }
}
```
**Class OnTransportState**
```
package state;

/**
 *
 * @author rainer
 */
public class OnTransportState implements PackageState {

    // Singleton Pattern
    private static final OnTransportState instance = new OnTransportState();

    public static OnTransportState instance() {
        return instance;
    }

    /**
     * State transition
     *
     * @param pak
     */
    @Override
    public void updateState(Package pak) {
        System.out.println("Parcel is on its way...next step is delivery");
        pak.setCurrentState(InDeliveryState.instance());
    }
}
```
**Class InDeliveryState**
```
package state;

/**
 *
 * @author rainer
 */
public class InDeliveryState implements PackageState {

    // Singleton Pattern
    private static final InDeliveryState instance = new InDeliveryState();

    public static InDeliveryState instance() {
        return instance;
    }

    /**
     * State transition
     *
     * @param pak
     */
    @Override
    public void updateState(Package pak) {
        System.out.println("Parcel will be delivered soon... the next step is handover");
        pak.setCurrentState(DeliveredState.instance());
    }
}
```
**Class DeliveredState**
```
package state;

/**
 *
 * @author rainer
 */
public class DeliveredState implements PackageState {

    // Singleton Pattern
    private static final DeliveredState instance = new DeliveredState();

    public static DeliveredState instance() {
        return instance;
    }

    /**
     * State transition
     *
     * @param pak
     */
    @Override
    public void updateState(Package pak) {
        System.out.println("Package is delivered...thank you for your trust;-)");
    }
}
```
**Class Package**
```
package state;

/**
 *
 * @author rainer
 */
public class Package {

    private PackageState currentState;
    private String packageId;

    public Package(PackageState currentState, String packageId) {
        
        super();
        this.currentState = currentState;
        this.packageId = packageId;

        if (currentState == null) {
            this.currentState = HandedInState.instance();
        }
    }

    public PackageState getCurrentState() {
        return currentState;
    }

    public void setCurrentState(PackageState currentState) {
        this.currentState = currentState;
    }

    public String getPackageId() {
        return packageId;
    }

    public void setPackageId(String packageId) {
        this.packageId = packageId;
    }

    public void update() {
        currentState.updateState(this);
    }
}
```
**Class State - main()**
```
package state;

/**
 *
 * @author rainer
 */
public class State {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {

        Package pak = new Package(null, "4711");

        pak.update();
        pak.update();
        pak.update();
        pak.update();
    }
}
```
**Output**
```
run:
The package has been handed over...the next step is transport to the destination
Parcel is on its way...next step is delivery
Parcel will be delivered soon... the next step is handover
Package is delivered...thank you for your trust;-)
BUILD SUCCESSFUL (total time: 0 seconds)
```













































