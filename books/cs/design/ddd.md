# modeling
* Carefully distilling and constraining the model's associations by simplifying models relationships, i.e. pushing bidirectional many-to-many to unidirectional one-to-one. > The fewer and simpler the associations in the model, the better.
## entities
* > ENTITY is an abstract continuity threading through a life cycle and even passing through multiple forms. Some objects are not defined primarily by their attributes. They represent a thread of identity that runs through time and often across distinct representations. Sometimes such an object must be matched with another object even though attributes differ. An object must be distinguished from other objects even though they might have the same attributes. Mistaken identity can lead to data corruption.
* > An object defined primarily by its identity is called an ENTITY
* entity can be without natural identifier or even common attributes, i.e. bank transaction
* > When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects by attributes. Define an operation that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitrary identifier created by and for the system, but it must correspond to the identity distinctions in the model. The model must define what it means to be the same thing.
* > the most basic responsibility of ENTITIES is to establish continuity so that behavior can be clear and predictable
operation  
## value objects
* > An object that represents a descriptive aspect of the domain with no conceptual identity is called a VALUE OBJECT.
* > VALUE OBJECTS can reference ENTITIES
* > When you care only about the attributes of an element of the model, classify it as a VALUE OBJECT. Make it express the meaning of the attributes it conveys and give it related functionality. Treat the VALUE OBJECT as immutable. Don't give it any identity and avoid the design complexities necessary to maintain ENTITIES.
* The attributes that make up a VALUE OBJECT should form a conceptual whole
## services
* > A SERVICE is an operation offered as an interface that stands alone in the model, without encapsulating state, as ENTITIES and VALUE OBJECTS do.
* A good SERVICE has three characteristics.
  * The operation relates to a domain concept that is not a natural part of an ENTITY or VALUE OBJECT.
  * The interface is defined in terms of other elements of the domain model.
  * The operation is stateless. Statelessness here means that any client can use any instance of a particular SERVICE without regard to the instance's individual history.
##  modules
* there should be low coupling between MODULES and high cohesion within them
## aggregates 
* > Cluster the ENTITIES and VALUE OBJECTS into AGGREGATES and define boundaries around each. Choose one ENTITY to be the root of each AGGREGATE, and control all access to the objects inside the boundary through the root. Allow external objects to hold references to the root only. Transient references to internal members can be passed out for use within a single operation only. Because the root controls access, it cannot be blindsided by changes to the internals. This arrangement makes it practical to enforce all invariants for objects in the AGGREGATE and for the AGGREGATE as a whole in any state change.
# factories
* > Shift the responsibility for creating instances of complex objects and AGGREGATES to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Provide an interface that encapsulates all complex assembly and that does not require the client to reference the concrete classes of the objects being instantiated. Create entire AGGREGATES as a piece, enforcing their invariants.
* basic requirements for any good FACTORY are Each creation method is atomic and enforces all invariants of the created object or AGGREGATE. A FACTORY should only be able to produce an object in a consistent state. For an ENTITY, this means the creation of the entire AGGREGATE, with all invariants satisfied, but probably with optional elements still to be added. For an immutable VALUE OBJECT, this means that all attributes are initialized to their correct final state. If the interface makes it possible to request an object that can't be created correctly, then an exception should be raised or some other mechanism should be invoked that will ensure that no improper return value is possible.
1.
The FACTORY should be abstracted to the type desired, rather than the concrete class(es) created. The sophisticated FACTORY patterns in Gamma et al. 1995 help with this.
* When designing the method signature of a FACTORY, whether standalone or FACTORY METHOD, keep in mind these two points.
Each operation must be atomic. You have to pass in everything needed to create a complete product in a single interaction with the FACTORY. You also have to decide what will happen if creation fails, in the event that some invariant isn't satisfied. You could throw an exception or just return a null. To be consistent, consider adopting a coding standard for failures in FACTORIES.
The FACTORY will be coupled to its arguments. If you are not careful in your selection of input parameters, you can create a rat's nest of dependencies. The degree of coupling will depend on what you do with the argument. If it is simply plugged into the product, you've created a modest dependency. If you are picking parts out of the argument to use in the construction, the coupling gets tighter.
