# OOPs #

## Abstraction ##
Class abstraction is the separation of class implementation from the use of a class. The details of implementation are encapsulated and hidden from the user. This is known as class encapsulation. A class is also known as Abstract Data Type (ADT). 

This is achieved in java through the use of abstract classes and interfaces. They only provide the contract without providing any implementation details. 

### What is a class contract? ###
The collection of methods and fields that are accessible from outside the class, together with the description of how these members are expected to behave, serves as the class's contract. 

## Encapsulation ##

Encapsulation allows hiding the internal representation of an object from outside view and access. It prevents unauthorized parties from directly altering object data, ensuring data consistency. Declaring class variables and methods as private is essential for encapsulation. 


## Polymorphism ##
Polymorphism means that a variable of the supertype can refer to a subtype object. The inheritance relationship enables a subclass to inherit features from its superclass with additional new features. A subclass is a specialization of its superclass. Every instance of a subclass is also an instance of its superclass, but not vice-versa. An object of a subclass can be used whereever its superclass object is used. This is commonly known as Polymorphism. In simple terms, polymorphism means an object of a supertype can refer to a subtype object. 

### Dynamic Binding ###
A method can be implemented in several classes along the inheritance chain. The JVM decides which method is invoked at runtime. 
There are two terms: A declared type and an actual type. The type that declares a variable is called as the declared type of the variable. The instance may be created using the constructor of the declared type or its subtype. The actual class of the variable is the actual class for the object referenced by the variable. Which method must be invoked by an object is determined by the object's actual type. ----- This is known as Dynamic Binding. 

> Matching a method signature and binding a method implementation are two separate issues. 

- The method signature:
    The declared type of the reference variable decides which method to match at compile time. The compiler finds a matching method according the parameter type, number of parameters, and the order of parameters at compile time. 
- Binding a method implementation: 
    A method may be implemented in several classes along the inheritance chain. The JVM dynamically binds the implementation of the method at runtime, decided by the actual type of the variable.  

### Constructor Chaining ###
A constructor may invoke an overloaded constructor or its superclass constructor. If neither is invoked explicitly, the compiler automatically puts super() as the first statement in the constructor. 

> In any case, constructing an instance of a class invokes the constructors of all the superclasses along the inheritance chain. 
When constructing an object of a subclass, the subclass constructor first invokes its superclass constructor before performing its own tasks. This process of invoking the superclass constructor continues until the last constructor along the inheritance hierarchy is called. This is called constructor chaining. 