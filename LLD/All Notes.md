
SOLID Principles 

Problems:

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




SOLID:

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
	