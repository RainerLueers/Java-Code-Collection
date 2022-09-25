---
title: Java - Code Collection
---  
# Immutable

Ein Objekt ist unveränderlich, wenn sich sein Zustand nach seiner Erstellung nicht 
ändert. Folglich ist eine Klasse unveränderlich, wenn ihre Instanzen unveränderlich sind. 
Das **Immutable Pattern** erhöht die Robustheit von Objekten, die Verweise auf 
dasselbe Objekt teilen, und reduziert den Overhead des gleichzeitigen Zugriffs auf 
ein Objekt. 

**Class Car is immutable**
```
/*
 * Java-Code-Collection
 * @version: 24.02.2022
 * @copyright © 2022 Rainer Lüers - all rights reserved
 */
package immutable;

/**
 *
 * @author rainer
 */
public final class Car {

    private final String brand;
    private final String model;
    private final int horsePower;
    private final int cubicCapacity;

    public Car(String mBrand, String mModel, int mHorsePower, int mCubicCapacity) {
        brand = mBrand;
        model = mModel;
        horsePower = mHorsePower;
        cubicCapacity = mCubicCapacity;
    }

    public String getBrand() {
        return brand;
    }

    public String getModel() {
        return model;
    }

    public int getHorsePower() {
        return horsePower;
    }

    public int getCubicCapacity() {
        return cubicCapacity;
    }
}

```
**Class Immutable - main()**
```
package immutable;

/**
 *
 * @author rainer
 */
public class Immutable {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {

        Car car = new Car("Porsche", "911 Carrera", 200, 3000);

        System.out.println(
                car.getBrand() + "\n"
                + car.getModel() + "\n"
                + car.getHorsePower() + " PS" + "\n"
                + car.getCubicCapacity() + " ccm");
    }
}
```
**Output**
```
run:
Porsche
911 Carrera
200 PS
3000 ccm
BUILD SUCCESSFUL (total time: 0 seconds)
```























