----------------------------------------------------------------------------------------------------------------
Title: The Bridge Pattern

Sources:
Notes below regarding proxy pattern taken from "Design Patterns - Elements of Reusable Object-Oriented Software"
By Gamma, Helm, Johnson, Vlissides

Example Code provided by Derek Banas:
Tutorial: https://www.youtube.com/watch?v=9jIgSsIfh_8
Source Code: http://www.newthinktank.com/2012/10/bridge-design-pattern-tutorial/

Author: Justin J

Purpose: FAU Object Oriented Software Design Course, Sprint 2017

----------------------------------------------------------------------------------------------------------------

Intent
- Decouple an abstraction from its implementation so that the two can vary independently

Motivation
- when abstraction can have one of several possible implementations, the usual way to accommodate them is to use inheritence
- abstract class defines the interface to the abstraction, and the concrete subclasses implement it in different ways
	- this approach is sometimes not flexible enough
- inheritance binds implementation to the abstraction permanently, making it difficult to modify/extend/reuse abstractions
  and implementations independently
- to bridge the abstraction and its implementation so that they may vary independently

Applicability
- to avoid a permanent binding between an abstraction and its implementation. This may be the case when the implementation
  must be selected or changed at run-time
- both abstractions and implementations should be extensible by subclassing. Bridge lets you combine the different abstractions
  and implementations and extend them independently
- changes in implementation of an abstraction should have no impact on clients, their code should not have to be recompiled
- to hide implementation of an abstraction completely from clients
- to share an implementation among multiple objects, a fact that should be hidden from client.

Structure
- see BridgePatternDiagram.png

Participants
- Abstraction
	- defines abstraction's interface
	- maintains a reference to an object of type Implementor
- RefinedAbstraction
	- extends the interface defined by abstraction
- Implementor
	- defines the interface for implementation classes. This interface desn't have to correspond exactly to Abstraction's interface,
	  in fact the two interfaces can be quite different
	- Typically Implementor interface provides only primitive operations, and Abstraction defines higher level operations based on
	  these primitives
- ConcreteImplementor
	- implements the Implementor interface and defines its concrete implementation
	
Collaborations
- abstraction forwards client requests to its Implementor object

Consequences
- decoupling interface and implementation, implementation is not bound permanently to an interface. 
	- this eliminates compile time dependencies on the implementation
	- encourages layering that can lead to a better structured system, high level part of system only has to know about Abstraction
	 and Implementor
- improved extensibility - you can extend the abstraction and implementor hierarchies independently
- hiding implementation details from clients, you can shield clients from implementation details

Implementation
- Only one Implementor: when only one implementation, creating an abstract Implementor class isn't necessary. 
- Creating the right Implementor object
	- if abstraction knows about all ConcreteImplementor classes, then it can instantiate one of them in its constructor, it can decide
	  between them based on parameters passed to its constructor. If for example a collection class supports multiple implementations, the
	  decision can be based on the site of the collection. A linked list implementation can be used for small collections and hash table for larger
	- another approach is to choose a default implementation initially and change it later according to usage. It's also possible to delaget 
	  the decision to another object altogether. 
- Sharing implementors
- Using multiple inheritence

Related Patterns
- abstract factory
- adapter pattern