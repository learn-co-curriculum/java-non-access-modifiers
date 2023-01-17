# Non-access Modifiers

## Learning Goals

- Create a static variable to store class state
- Use the Java Visualizer to model class and object state
- Create a final variable to prevent reassignment after initialization

## Introduction

In the previous lesson, we learned about **access modifiers**. We've seen
other types of keywords used other than the access modifier keywords though.
For example:

`public static void main(String[] args`

In this lesson we will focus on the next keyword `static` and what that means.

## What are Non-Access Modifiers?

Non-access modifiers apply to classes, methods, fields and constructors and
indicate their desired behavior to the compiler.

Here is the list of non-access modifiers that are in scope for this discussion:

1. `static` - static variables and methods are also called "class" variables or
   methods because they do not require an instance of the class to be used.
2. `final` - final classes, methods or variables mean that they cannot be
   modified, which manifest itself different for classes, methods and
   variables.

## Static

A `static` member of a class (i.e. a variable or a method) is a member that
can be accessed directly on the class without needing an instance of that
class to be created. This is usually the case when we describe something about
the class that will be true for all instances of that class.

In Java, any class that we want to be able to run from the command line needs to
have a `public` (i.e. fully accessible)`static` (i.e. accessible through the
class, without an object) method called `main` because the JVM needs to be able
to call it without an object since it doesn't know anything about the values that
might be required to properly create an instance.

Let's look at an example using a `Cat` class with each
cat having a name and favorite toy.  We will also add
a `static` variable to keep track of the cat `population`.
Each time we create a new `Cat` instance, we will
increase the population value by 1:

```java
public class Cat {
   private String name;
   private String favoriteToy = "catnip ball";
   private static int population ;

   public static void main(String[] args) {
      Cat cat1 = new Cat();
      Cat.population++;
      cat1.name = "Purrl";

      Cat cat2 = new Cat();
      Cat.population++;
      cat2.name = "Honey";
      cat2.favoriteToy = "squeaky mouse";

   }

} 
```

Notice that we use dot notation to access the `population` field,
but we use the class name rather than an object reference:

`Cat.population++;`

Let's use the Java Visualizer to see where static variables are stored.
Unfortunately, IntelliJ's Java Visualizer does not show static variables,
but we can use the browser-based visualizer at
[https://pythontutor.com/java.html](https://pythontutor.com/visualize.html#code=public%20class%20Cat%20%7B%0A%20%20%20%20String%20name%3B%0A%20%20%20%20String%20favoriteToy%20%3D%20%22catnip%20ball%22%3B%0A%20%20%20%20static%20int%20population%20%3B%0A%0A%20%20%20%20public%20static%20void%20main%28String%5B%5D%20args%29%20%7B%0A%20%20%20%20%20%20%20%20Cat%20cat1%20%3D%20new%20Cat%28%29%3B%0A%20%20%20%20%20%20%20%20Cat.population%2B%2B%3B%0A%20%20%20%20%20%20%20%20cat1.name%20%3D%20%22Purrl%22%3B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20Cat%20cat2%20%3D%20new%20Cat%28%29%3B%0A%20%20%20%20%20%20%20%20Cat.population%2B%2B%3B%0A%20%20%20%20%20%20%20%20cat2.name%20%3D%20%22Honey%22%3B%0A%20%20%20%20%20%20%20%20cat2.favoriteToy%20%3D%20%22squeaky%20mouse%22%3B%0A%0A%20%20%20%20%7D%0A%0A%7D%0A&cumulative=false&heapPrimitives=nevernest&mode=edit&origin=opt-frontend.js&py=java&rawInputLstJSON=%5B%5D&textReferences=false)



| Code                                                        | Java Visualizer                                                                                         |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Static variable is initialized<br>when the class is loaded. | ![step 0](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step0.png) |
| `Cat cat1 = new Cat();`                                     | ![step 1](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step1.png) |
| `Cat.population++;`                                         | ![step 2](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step2.png) |
| `cat1.name = "Purrl";`                                      | ![step 3](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step3.png) |
| `Cat cat2 = new Cat();`                                     | ![step 4](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step4.png) |
| `Cat.population++;`                                         | ![step 5](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step5.png) |
| `cat2.name = "Honey";`                                      | ![step 6](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step6.png) |
| `cat2.favoriteToy = "squeaky mouse";`                       | ![step 7](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/static_step7.png) |


Notice in the screen prints the static variable `population` is **not** stored in any of the `Cat` objects.

- Each `Cat` object has its own copy of the instance variables `name` and `favoriteToy`.
- There is only one copy of the static variable `population`.


Since the static variable `population` is not stored with any `Cat` objects,
we can actually use the variable before creating a `Cat` instance!

For example, let's print the population at the beginning and end of the `main()` method:

```java
public static void main(String[] args) {
        System.out.println("Initial cat population = " + Cat.population);
        Cat cat1 = new Cat();
        Cat.population++;
        cat1.name = "Purrl";

        Cat cat2 = new Cat();
        Cat.population++;
        cat2.name = "Honey";
        cat2.favoriteToy = "squeaky mouse";

        System.out.println("Final cat population = " + Cat.population);
    }
```

The program prints:

```text
Initial cat population = 0
Final cat population = 2
```

## Accessing A Static Variable Through An Object Reference

In general, it is best to access a static variable using the class reference.  When
we see a class name in front of the dot `.`, it makes it clear that the variable
must be static.  We can however access a static variable through an object reference
after creating a class instance, but this is generally not considered a good coding practice.

| Do This             | Don't Do This        |
|---------------------|----------------------|
| `Cat.population++;` | `cat1.population++;` |


## Viewing Static Variables in IntelliJ

As previously mentioned, IntelliJ's Java Visualizer does not show static variables.

![intellij java visualizer no static variables](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/intellij_nostatic.png)


However, we can view static variables in the Debugger Variable Panel.
Unfortunately, the debugger view displays the static variable `population`
as part of the state of each `Cat`, which is misleading. 

![intellij debugger static variables](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/intellij_debugger_static.png)


It is important to remember
there is only one copy of the static variable `population`, and it **IS NOT** stored
with any of the `Cat` objects!

## Final Variables

Let's assume all of our objects represent domestic cats, which belong to the
species "Felis catus".  We can use a static variable to store the value:

`private static String species = "Felis catus";`

This is great that we have one copy of the value that can be shared by all
`Cat` instances:

![species not final variable](https://curriculum-content.s3.amazonaws.com/6676/java-mod2-oop-fundamentals/species_not_final.png)

However, it is currently possible to modify the static `species` variable
in the `main()` method. For example, we could reassign the variable and turn all cats into dogs!

```java
public static void main(String[] args){
    Cat.species="Canis familiaris";
    ...
}
```

Thankfully, Java has a modifier named `final` that tells the compiler to prevent
reassignment once the variable has been initialized.
It is often used in conjunction with the `static` modifier to
handle **constants**. A **constant variable** is defined as a variable that
cannot be modified after being initialized and can be called upon without an
instance of the class.

```java
private static final String SPECIES = "Felis catus";
```

So we can access the final variable in the `main()` method, but we can't reassign the value:

| OK                                 | Compiler Error                    |
|------------------------------------|-----------------------------------|
| `System.out.println(Cat.SPECIES);` | `Cat.SPECIES="Canis familiaris";` |


Note that when constants are defined, in Java, we usually depict constants with
a variable name in all capital letters `SPECIES`. We use underscores for separation of
multiple words such as `AVERAGE_LIFESPAN`.

One other thing to note is that constants are often used by other classes.
If this is the case, the variable should be declared with the public modifier:

```java
public static final String SPECIES = "Felis catus";
```

- `public` : We can access the constant `Cat.SPECIES` in any class
- `static` : We can access the variable without needing to instantiate a `Cat` instance
- `final` : We cannot modify its value after initialization, which means it's a constant value that we can rely on


## Conclusion

The `static` keyword is used to declare a class variable, meaning there is a single copy of the variable
that can be shared among all class instances and is available even before an instance is created.

The `final` keyword is used to prevent variable reassignment after initialization.

We combine `final` and `static` to create a constant.  Constants are often also made `public`
to allow use by other classes.
