
#Problems:

Code maintainability : Not easy to integrate new features
Code readability : tightly coupled code, so very difficult to understand, new commers will have many problems
Bugs Introduction: A very coupled structure would cause a lot of erros if any of its smaller code breaks.

A Big and well framed class name, reduces redundancy and actually explains the name of the  

UML:

## **Composition**

### **Definition**

- **Composition** is a **strong “has-a” relationship** between two classes.
    
- It represents **whole-part ownership**, where:
    
    - The **part cannot exist without the whole**.
        
    - If the whole is destroyed, all its parts are destroyed automatically.
        

Think of it as a “death relationship” — parts die with the whole

### **Difference from Aggregation**

|Feature|Aggregation|Composition|
|---|---|---|
|Ownership|Weak “has-a”|Strong “owns-a”|
|Lifespan of part|Can exist independently|Cannot exist independently|
|UML Symbol|Hollow diamond|Filled diamond|

- **Example:**
    
    - Aggregation → `Library` has `Books` (books can exist outside library).
        
    - Composition → `Car` has `Engine` (engine doesn’t exist without car).


|Relationship|Lifespan|UML Symbol|Example|Description|
|---|---|---|---|---|
|**Association**|Independent|Plain line|Teacher–Student|Weakest link, just interaction|
|**Aggregation**|Independent|Hollow diamond|Department–Professor|“Has-a”, but shared part|
|**Composition**|Dependent|Filled diamond|Car–Engine|“Has-a”, but owned part|

#SOLID:

S: Single Responsibility Principle (SRP)
O : Open close principle
L : Liskov Substitution principle (LSP)
I : Interface segregation principle
D : Dependency inversion principle 

Single Responsibility Principle

	A class should have only one reason to change
	no multiple responsibility for a single class
	 
	How Composition Helps

       Composition allows you to delegate responsibilities to separate classes and       make your main class simpler. Split responsibilities into smaller classes

	getter and setter are good practices while create classes
	
	Composition usually → one-way reference.
 
        In most cases, the **whole (Car)** knows about its parts(Engine`,`AudioSystem`, `Sunroof`).
	    
	 The **parts don’t need to know** about the whole unless absolutely required.
		  
	
		When should a part reference the whole?**
		- Sometimes a part needs context from the whole. Example:
	    
	    - `AudioSystem` might want to **check if Car’s engine is ON before playing music**.
	        
	    - In that case, `AudioSystem` might keep a reference to `Car` (but it creates tight coupling

Open Close Principle
	A class should open for extension but close for modification
	
	In OOP, **polymorphism** allows you to write code that works with **objects of different types through a common interface** (usually the parent class).

	A parent class reference can point to a child class object.

	A usual way of eliminating the open close is that define a interface class, which just defines the function names, and seperate child classes for the methods:
		Like: 
			A database abstract class with saving method to multiple types of db 
			can be changed to:
			A parent db interface just has a save function/method. child classes for saving to sql, mongodb, cassandra, properly defining their own functionality.

			A parent class ref can be used to its child object.
			So, d:db = SaveToSql(), d can access child class methods
			d.save will actually save the db to SQL. and similarly we can have multiple databases class and we can just use parent reference to point them and use the same method, i.e save one.

Liskov Substitution Principle:

	Subclasses should be substitutable for their base classes, child should implement at-least the parent methods and may increase it.
	
	Code Breaks when for e.g. there is a parent account class, a child class it just a fixed deposit account class, and we cannot have withdraw from a FD account, so the child class cannot be substituted here for the base class.
	
	doing a coupling from client side, like a condition that if the account type is FD, then there is no option to call for withdraw, makes it coupled and is not a good practice. (This modifies the client side code, so straight breaks the O principle )Client should directly talk to the interface (base abstracted class) and further routing should be set from there
	
	**Better Way**:
	
	FD should never be a child to account class as its decreasing the functionality of its parent.
	Create a abstract class named: NonwithdrawsAccount and WithdrawsAccount.
	FD extends the NonWithdraw one while savings, checkin extends the Withdraw one.
	
	Guide Lines:
	
	if user/client calls on some function on a class, then method on that class and its child classes can be called. the methods that are parent to the class, cannot be called as they could have less functionality and child always has atleast same functions of the parent.
	
	so in short return current or narrower and not broader one.
	
	Similarly for exceptions, if a parent method defines, lets say a logic error
	then its child cannot throw exception which are from a different class and can only throw the child exception classes
	
	Child class should behave as the parent class
		term broad : parent
		term narrow : child
	 **==Precondition Rule in LSP==**
	
  	A subclass **must not strengthen** the preconditions of its parent class.
	
	 🔹 Meaning:
	
	If the parent allows some inputs,  
	the child **must also accept at least those same inputs (or more)**.
	
	It **cannot** add new restrictions that make the method harder to call.

	Or, It may strengthen the Post Condition, 
	LSP says:  A subclass can make fewer demands (weaker preconditions) and offer stronger guarantees (stronger postconditions) — but never the opposite.

	For example, there is a premium account and a normal account, which has a limit of $100 on an account.

Interface Segregation Principle

	Many client specific interface is better than one general purpose interface
	Client should not implement methods they don't need.

	So just make a different class where clients only need to implement methods that are needed for them and nothing else.

Dependency Inversion Principle
	High level module should not depend on low level module but rather both should depend on
	Abstraction.

	So lets say we have 2 db and application layers calls it to interact and save data. But thats high level and Low level (server) things interact directly,
	What we can do it add a class Persistence between them:

	Persistence p has this method called save, and all those Databases references, So if new database is added, Persistence p dynamically can reference to its child class object of new_database. and it also has save method overided. 

	and so, we have an interface now betwwen High level and low level

	If Open Close is the target, dependency inversion is the solution



Build Google Docs

