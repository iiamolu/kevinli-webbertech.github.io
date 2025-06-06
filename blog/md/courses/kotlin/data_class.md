# Class

## Data Class

A data class is a special type of class primarily used for holding data. It’s designed to simplify the process of creating classes used to represent and manipulate data objects.

Data classes automatically provide us with various functionalities, reducing the amount of boilerplate code required. Firstly, let’s see the definition of a data class:

`data class Person(val name: String, val age: String)`

The data class provides the automatic generation of common functions such as equals(), hashCode(), and toString(), which are based on the properties defined in the class.

Let’s initialize two instances of the Person data class with the same properties and see if the functions exist:

```java
val person1 = Person("Ada", "31")
val person2 = Person("Ada", "31")
assertEquals(true, person1.equals(person2))
assertEquals(person1.hashCode(), person2.hashCode())
assertEquals(person1.toString(), person2.toString())
```

It also supports destructuring declaration, which means that we can extract and assign the properties of an object or a data class to separate variables in a single statement:

```java
val (name, age) = person1
assertEquals("Ada", name)
assertEquals("31", age)
```

Data class also has a copy() function, which can be used to create a copy of an object, optionally allowing the modification of specific properties during the copy process:

`val person3 = person1.copy()`

assertEquals(person1.toString(), person3.toString())

## Object

In Kotlin, objects are used to create singleton instances or to group related functionality. We can effortlessly access and utilize the singleton instance’s objects without requiring explicit singleton patterns or static declarations.

It’s handy to use objects to maintain a global state, provide centralized functionality, or handle application-wide operations.

```java
object PersonManager {
    private val personList = mutableListOf<Person>()

    fun addPerson(person: Person) {
        personList.add(person)
    }

    fun removePerson(person: Person) {
        personList.remove(person)
    }

    fun getAllPersons(): List<Person> {
        return personList.toList()
    }
}
```

We declared an object to manage a list of people, and now we can manage a person list with a static method:

```java
val person1 = Person("Ada", "31")
val person2 = Person("Chris", "30")

PersonManager.addPerson(person1)
PersonManager.addPerson(person2)
assertEquals(2, PersonManager.getAllPersons().size)
```

**anonymous**

Another way to use objects is by expression. Object expressions provide a way to create anonymous objects on the fly, extending existing classes or interfaces and adding additional functionality as needed.

Firstly, let’s declare a new class that has one function and can be inherited:

```java
open class Employee(val name: String, val department: String) {
    open fun greeting() = "Hi! My name is $name. I work in $department department"
}
```

Then, let’s create an anonymous Person object:

```java
val boss = object : Employee("Jack", "IT") {
    override fun greeting() = "I'm $name. I work in $department department and I'm the boss"
}

assertEquals("I'm Jack. I work in IT department and I'm the boss", boss.greeting())
```

 Differences Between Data Class and Object

**Let’s compare and contrast some key features:**

|Data class|	Object|
|-----|-------|
|Purpose|Holding data, data manipulation|Group related functionality|
|Number of instances|Multiple|Single|
|Autogenerated methods|	equals(), hashCode(), toString(), copy()|None|
|Deconstructing declaration|Yes|No|

## Ref

- https://kotlinlang.org/docs/object-declarations.html
- https://www.baeldung.com/kotlin/object-vs-data-class