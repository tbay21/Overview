# Course Overview

## 1. Abstract Class

An abstract class is a class declared with the `abstract` keyword. It provides a common structure for related subclasses and can contain both abstract and concrete methods. An abstract method has no implementation in the parent class and must be implemented by a concrete subclass.

For example, the `Bentuk` class in the `Inheritance_and_Polymorphism` project provides a common structure for different shapes. It contains the `warna` attribute and methods shared by its subclasses.

```java
public abstract class Bentuk {
    protected String warna;

    public Bentuk(String warna) {
        this.warna = warna;
    }

    public abstract double hitung();
}
```

If `Bentuk` is declared as an abstract class, subclasses such as `BujurSangkar` and `Lingkaran` must implement the `hitung()` method.

## 2. Interface

An interface defines a contract that specifies methods a class must implement. It allows different classes to provide their own implementations of common operations without requiring them to share the same parent class.

For example, an interface named `Calculable` could define a common calculation method.

```java
public interface Calculable {
    double hitung();
}
```

Classes can implement this interface using the `implements` keyword.

```java
public class BujurSangkar implements Calculable {
    private double sisi;

    public BujurSangkar(double sisi) {
        this.sisi = sisi;
    }

    @Override
    public double hitung() {
        return sisi * sisi;
    }
}
```

The `hitung()` method calculates the square's area. Other classes could implement the same interface to perform different calculations.

## 3. Arrays

An array is a data structure that stores multiple elements of the same type in a fixed-size collection. Arrays can store primitive values or references to objects.

For example, the `Bank` class in the `ArrayList` project uses an array to store customer objects.

```java
private Customer[] customers;
private int numberOfCustomers;

public Bank() {
    this.customers = new Customer[10];
    this.numberOfCustomers = 0;
}
```

The `customers` array can store up to 10 customer objects, while `numberOfCustomers` tracks the number of registered customers.

The `addCustomer()` method adds a new customer to the next available position.

```java
public void addCustomer(
    String firstName,
    String lastName,
    String accountNumber
) {
    if (this.numberOfCustomers < this.customers.length) {
        this.customers[this.numberOfCustomers] =
            new Customer(firstName, lastName, accountNumber);

        this.numberOfCustomers++;
    }
}
```

The `findCustomer()` method searches for a customer by account number using a loop.

```java
public Customer findCustomer(String accountNumber) {
    for (int i = 0; i < this.numberOfCustomers; i++) {
        if (this.customers[i].getAccountNumber()
                .equals(accountNumber)) {
            return this.customers[i];
        }
    }

    return null;
}
```

This example demonstrates how arrays can be used to store, access, and search for objects. Unlike an `ArrayList`, a regular array has a fixed length after initialization.

## 4. Inheritance

Inheritance allows a class to acquire attributes and methods from another class. In Java, inheritance between classes is implemented using the `extends` keyword.

For example, the `Inheritance_and_Polymorphism` project contains the following class hierarchy:

- `BujurSangkar` extends `Bentuk`.
- `Lingkaran` extends `Bentuk`.
- `Silinder` extends `Lingkaran`.

The following code demonstrates inheritance:

```java
public class BujurSangkar extends Bentuk {
    private double sisi;

    public BujurSangkar(double sisi, String warna) {
        super(warna);
        this.sisi = sisi;
    }
}
```

The `BujurSangkar` class inherits the `warna` attribute and the accessible methods of `Bentuk`. The `super(warna)` statement calls the parent class constructor to initialize the color.

Similarly, `Silinder` extends `Lingkaran`, allowing it to reuse the radius-related functionality and color information inherited through the class hierarchy.

Inheritance promotes code reuse and establishes relationships between classes.

## 5. Polymorphism

Polymorphism allows objects of different classes to be accessed through a common parent-class reference while providing different implementations of the same method. In Java, runtime polymorphism can be achieved through method overriding.

In the `Inheritance_and_Polymorphism` project, the `BujurSangkar`, `Lingkaran`, and `Silinder` classes override the `hitung()` method to perform different calculations.

**BujurSangkar:**

```java
@Override
public double hitung() {
    return sisi * sisi;
}
```

This method calculates the area of a square.

**Lingkaran:**

```java
@Override
public double hitung() {
    return PHI * radius * radius;
}
```

This method calculates the area of a circle.

**Silinder:**

```java
@Override
public double hitung() {
    return super.hitung() * tinggi;
}
```

This method calculates the cylinder's volume by multiplying the base area by its height.

Polymorphism is demonstrated in `Main.java`, where objects of different shape classes are stored in an array of type `Bentuk`.

```java
Bentuk[] daftarBentuk = {
    new BujurSangkar(sisi, warnaBS),
    new Lingkaran(radius, warnaL),
    new Silinder(tinggi, radiusS, warnaS)
};

for (Bentuk b : daftarBentuk) {
    System.out.println(
        b.getClass().getSimpleName() + " = " + b.hitung()
    );
}
```

Although the variable `b` is declared as type `Bentuk`, Java executes the overridden `hitung()` method according to the actual object type.

For a `BujurSangkar` object, the method calculates the square's area. For a `Lingkaran` object, it calculates the circle's area. For a `Silinder` object, it calculates the cylinder's volume.

This demonstrates runtime polymorphism through a common calculation method. It also shows how inheritance and method overriding work together to provide different behaviors through a shared parent-class reference.
