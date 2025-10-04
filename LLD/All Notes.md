
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

Subclasses should be substitutable for their base classes, child should implement atleast the parent methods and may increase it.

Breaks like when parent is account class, and a child class it just a fixed deposit account class, and we cannot have withdraw from a FD account, so the child class cannot be substituted here for the base class.

doing a coupling from client side, like a condition that if the account type is FD, then there is no option to call for withdraw, makes it coupled and is not a good practice. (This modifies the client side code, so straight breaks the O principle )Client should directly talk to the interface (base abstracted class) and further routing should be set from there

**Better Way**:

FD should never be a child to account class as its decreasing the functionality of its parent.
Create a abstract class named: NonwithdrawsAccount and WithdrawsAccount.
FD extends the NonWithdraw one while savings, checkin extends the Withdraw one.


