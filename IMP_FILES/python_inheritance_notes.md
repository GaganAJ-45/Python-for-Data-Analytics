# Python OOP: Inheritance

## 1. Definition

**Inheritance** is an Object-Oriented Programming (OOP) feature that
allows a class (the **child** or **derived** class) to acquire
attributes and methods from another class (the **parent** or **base**
class).

Inheritance helps reuse existing code, extend functionality, and create
relationships between related classes.

## 2. Why Do We Need Inheritance?

Suppose `Teacher` and `Student` both need a `name`, `age`, and a method
to display those details. Without inheritance, the same code may be
repeated in both classes.

A shared parent class avoids this duplication.

### Without inheritance

``` python
class Teacher:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)


class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)
```

### With inheritance

``` python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(self.name, self.age)


class Teacher(Person):
    pass


class Student(Person):
    pass


teacher = Teacher("Ravi", 35)
student = Student("Arun", 20)

teacher.display()
student.display()
```

Output:

``` text
Ravi 35
Arun 20
```

`Teacher` and `Student` inherit the initializer and `display()` method
from `Person`.

## 3. Parent Class and Child Class

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  Parent class / Base class           The class whose attributes and
                                      methods are inherited

  Child class / Derived class         The class that inherits from
                                      another class
  -----------------------------------------------------------------------

Example:

``` python
class Animal:       # Parent / base class
    def eat(self):
        print("Eating")


class Dog(Animal):  # Child / derived class
    pass
```

The parentheses in `class Dog(Animal)` specify the parent class.

## 4. How Method Lookup Works

When an expression such as `dog.eat()` is evaluated, Python looks for
the requested attribute or method using the object's class and its
inheritance hierarchy. The order is defined by the **Method Resolution
Order (MRO)**.

``` python
class Animal:
    def eat(self):
        print("Animal is eating")


class Dog(Animal):
    pass


dog = Dog()
dog.eat()
```

Output:

``` text
Animal is eating
```

Inspect the MRO:

``` python
print(Dog.mro())
```

For this simple example, the order is:

``` text
Dog -> Animal -> object
```

The built-in `object` class is the ultimate base class of ordinary
Python classes.

## 5. Benefits of Inheritance

1.  **Code reusability:** Common attributes and methods can be defined
    once in a parent class.
2.  **Extensibility:** A child class can add its own attributes and
    methods.
3.  **Method overriding:** A child class can provide a specialized
    implementation of an inherited method.
4.  **Organization:** Related classes can be represented in a clear
    hierarchy.

## 6. Extending a Parent Class

A child class can use inherited methods and also define additional
methods.

``` python
class Animal:
    def eat(self):
        print("Eating food")


class Dog(Animal):
    def bark(self):
        print("Dog is barking")


dog = Dog()
dog.eat()   # Inherited method
dog.bark()  # Child class method
```

Output:

``` text
Eating food
Dog is barking
```

## 7. Method Overriding

**Method overriding** occurs when a child class defines a method with
the same name as an inherited method, providing its own implementation.

``` python
class Animal:
    def sound(self):
        print("Animal makes a sound")


class Dog(Animal):
    def sound(self):
        print("Dog barks")


animal = Animal()
dog = Dog()

animal.sound()
dog.sound()
```

Output:

``` text
Animal makes a sound
Dog barks
```

When `dog.sound()` is called, Python finds `sound()` in `Dog` first, so
the child implementation is used.

### Inheritance vs. Method Overriding

-   **Inheritance** establishes a relationship and makes parent
    functionality available to the child.
-   **Method overriding** lets the child customize an inherited method.

Overriding is an important foundation for polymorphism.

## 8. The `super()` Function

`super()` returns a proxy that delegates method calls to the next class
in the Method Resolution Order. It is commonly used in a child class to
call a parent class's initializer or another inherited method.

Consider:

``` python
class Person:
    def __init__(self, name):
        self.name = name


class Student(Person):
    def __init__(self, name, roll_number):
        super().__init__(name)
        self.roll_number = roll_number


student = Student("Arun", 101)

print(student.name)
print(student.roll_number)
```

Output:

``` text
Arun
101
```

### What happens in `super().__init__(name)`?

1.  `super()` provides access to the next class in the MRO.
2.  `.__init__(name)` calls that class's initializer.
3.  The parent initializer assigns `self.name = name`.
4.  The child initializer assigns `self.roll_number = roll_number`.

### Important constructor rule

If a child class defines its own `__init__()`, Python does **not**
automatically call the parent's `__init__()`.

``` python
class Parent:
    def __init__(self):
        self.x = 10


class Child(Parent):
    def __init__(self):
        self.y = 20


obj = Child()
print(obj.y)  # 20
print(obj.x)  # AttributeError: 'Child' object has no attribute 'x'
```

Call `super().__init__()` when the child needs the parent's
initialization logic:

``` python
class Child(Parent):
    def __init__(self):
        super().__init__()
        self.y = 20
```

## 9. Types of Inheritance in Python

### 9.1 Single Inheritance

One child class inherits from one parent class.

``` python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    pass
```

Structure:

``` text
Animal
  |
 Dog
```

### 9.2 Multilevel Inheritance

A class inherits from a class that itself inherits from another class.

``` python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    def bark(self):
        print("Barking")


class Puppy(Dog):
    def play(self):
        print("Playing")


puppy = Puppy()
puppy.eat()
puppy.bark()
puppy.play()
```

Structure:

``` text
Animal
  |
 Dog
  |
Puppy
```

A `Puppy` instance can access methods from `Puppy`, `Dog`, and `Animal`,
subject to normal attribute lookup.

### 9.3 Multiple Inheritance

One child class inherits from more than one parent class.

``` python
class Father:
    def skill1(self):
        print("Gardening")


class Mother:
    def skill2(self):
        print("Cooking")


class Child(Father, Mother):
    pass


child = Child()
child.skill1()
child.skill2()
```

Output:

``` text
Gardening
Cooking
```

Structure:

``` text
Father     Mother
    \       /
      Child
```

Multiple inheritance makes MRO especially important when parent classes
define methods with the same name.

### 9.4 Hierarchical Inheritance

Multiple child classes inherit from the same parent class.

``` python
class Animal:
    def eat(self):
        print("Eating")


class Dog(Animal):
    pass


class Cat(Animal):
    pass


dog = Dog()
cat = Cat()

dog.eat()
cat.eat()
```

Structure:

``` text
       Animal
       /    \
     Dog    Cat
```

### 9.5 Hybrid Inheritance

Hybrid inheritance combines two or more inheritance patterns, such as
multiple and multilevel inheritance.

Python supports hybrid inheritance. Complex hierarchies should be
designed carefully because method lookup can become difficult to reason
about.

## 10. Inheritance vs. Composition

Inheritance is appropriate for an **is-a** relationship. Composition is
often appropriate for a **has-a** relationship.

  Relationship          Example              Typical design
  --------------------- -------------------- ----------------
  A dog is an animal    `Dog` and `Animal`   Inheritance
  A car has an engine   `Car` and `Engine`   Composition

Example of composition:

``` python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()


car = Car()
car.start()
```

A car contains an engine; an engine is not a kind of car. Therefore,
composition is the more suitable relationship.

## 11. Key Points to Remember

-   Inheritance allows a child class to reuse and extend parent-class
    functionality.
-   The syntax is `class Child(Parent):`.
-   A child can use inherited methods without redefining them.
-   A child can add new attributes and methods.
-   A child can override inherited methods.
-   `super()` delegates to the next class in the MRO; it is not simply a
    hard-coded call to a named parent.
-   Defining a child `__init__()` does not automatically execute the
    parent `__init__()`.
-   Python supports single, multilevel, multiple, hierarchical, and
    hybrid inheritance.
-   Use inheritance for suitable **is-a** relationships; consider
    composition for **has-a** relationships.

## 12. Practice Questions

Try these without looking up the solutions immediately.

### Question 1 --- Basic Inheritance

Predict the output and explain why it appears even though `B` does not
define `display()`.

``` python
class A:
    def display(self):
        print("Class A")


class B(A):
    pass


obj = B()
obj.display()
```

### Question 2 --- Method Overriding

Predict the output. Why does Python execute the method in `B`?

``` python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        print("B")


obj = B()
obj.show()
```

### Question 3 --- Constructor Behavior

Identify which line raises an error and explain how `super()` can fix
it.

``` python
class A:
    def __init__(self):
        self.x = 10


class B(A):
    def __init__(self):
        self.y = 20


obj = B()

print(obj.x)
print(obj.y)
```

### Question 4 --- Build a Class Hierarchy

Create these classes:

-   `Employee`: stores `name` and `salary`.
-   `Manager`: inherits from `Employee` and adds `department`.
-   Use `super()` to initialize the inherited attributes.
-   Create a `Manager` object and print all three attributes.

### Question 5 --- Multilevel Inheritance

Create three classes: `Person`, `Employee`, and `Manager`.

-   `Person` stores a person's name.
-   `Employee` inherits from `Person` and stores an employee ID.
-   `Manager` inherits from `Employee` and stores a department.
-   Create a `Manager` object and access all three attributes.

------------------------------------------------------------------------

## 13. Interview Questions

1.  What is inheritance in Python?
2.  What is the difference between a parent class and a child class?
3.  What are the advantages of inheritance?
4.  What is method overriding?
5.  What is the purpose of `super()`?
6.  Does Python automatically call the parent constructor when a child
    defines its own `__init__()`?
7.  What is multiple inheritance?
8.  What is Method Resolution Order (MRO)?
9.  What is the difference between multilevel and multiple inheritance?
10. What is the difference between inheritance and composition?

**Recommended learning order:** Understand basic inheritance first, then
method overriding, constructor behavior, `super()`, inheritance
patterns, and finally MRO and the diamond problem.
