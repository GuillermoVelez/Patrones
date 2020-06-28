# Patrones de Diseño de Software
## Patrones de Creación
### 1. Fabrica Abstracta 
Se conoce también como abstract Factory, su objetivo principal es sportar multiples estandarees que sean establecidos por las diferentes jerarquias de herencia de objetos.
* Un sistema se configurara con una entre varias familias de productos
* Un conjunto de productos que estan relacionados, fueron hechos para utilizarse juntos 

![DiagramaAbstractFactory](imagenes/DiagramaAbstractFactory.png)

#### Elementos:
* **AngularJS** : Declara una interfaz para la creación de objetos de productos abstractos.
* **ConcreteFactory** : implementa las operaciones para la creacion de objetos de sus productos concretos.
* **AbstractProduct** : Crea una interfaz para los objetos de un determinado tipo de productos.
* **ConcreteProduct** : Fija el objeto de un producto perteneciente a la factoria concreta encargada de crear e implementar la interfaz del producto abstracto.
* **Client**: Utiliza las interfaces de la factoria y los productos abstractos.

#### Consecuencias:
* Las clases de implementación no son visibles para los clientes.
* Facilita el intercambio de familias de productos.
* Mejora el acoplamiento entre productos.

#### Código:

```java
public abstract class Disco implements Prototipo {
    @Override
    public abstract Prototipo clone();

    public abstract String getCapacidad();

    public abstract String getNombre();

    public abstract String getPrecio();

    @Override
    public String toString() {
            return getNombre() + " (" + getCapacidad() + ")";
    }
}
public abstract class DVD extends Disco {
...
}
public class DVD_CapaSimple extends DVD {

    @Override
    public Prototipo clone() {
            return new DVD_CapaSimple();
    }

    @Override
    public String getCapacidad() {
            return "4.7GB";
    }

    @Override
    public String getNombre() {
            return "DVD Capa Simple";
    }

    @Override
    public String getPrecio() {
            return "5.00$";
    }

}
public interface FabricaDiscos {

        public BluRay crearBluRay();
        public DVD crearDVD();
}
public class FabricaDiscos_CapaSimple implements FabricaDiscos {

       @Override
       public BluRay crearBluRay() {
               return new BluRay_CapaSimple();
       }

       @Override
       public DVD crearDVD() {
               return new DVD_CapaSimple();
       }

}
FabricaDiscos fabrica;
DVD dvd;
BluRay bluray;

fabrica = new FabricaDiscos_CapaSimple();
dvd = fabrica.crearDVD();
bluray = fabrica.crearBluRay();

System.out.println(dvd);
System.out.println(bluray);

fabrica = new FabricaDiscos_CapaDoble();
dvd = fabrica.crearDVD();
bluray = fabrica.crearBluRay();

System.out.println(dvd);
System.out.println(bluray);
 ```
Código tomado de: http://lineadecodigo.com/patrones/patron-abstract-factory/



