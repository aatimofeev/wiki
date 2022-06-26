# modeling
* Carefully distilling and constraining the model's associations by simplifying models relationships, i.e. pushing bidirectional many-to-many to unidirectional one-to-one. > The fewer and simpler the associations in the model, the better.
## entities
* > ENTITY is an abstract continuity threading through a life cycle and even passing through multiple forms. Some objects are not defined primarily by their attributes. They represent a thread of identity that runs through time and often across distinct representations. Sometimes such an object must be matched with another object even though attributes differ. An object must be distinguished from other objects even though they might have the same attributes. Mistaken identity can lead to data corruption.
* > An object defined primarily by its identity is called an ENTITY
* entity can be without natural identifier or even common attributes, i.e. bank transaction
* > When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. Be alert to requirements that call for matching objects by attributes. Define an operation that is guaranteed to produce a unique result for each object, possibly by attaching a symbol that is guaranteed unique. This means of identification may come from the outside, or it may be an arbitrary identifier created by and for the system, but it must correspond to the identity distinctions in the model. The model must define what it means to be the same thing.
* > the most basic responsibility of ENTITIES is to establish continuity so that behavior can be clear and predictable
operation  
# value objects
* > An object that represents a descriptive aspect of the domain with no conceptual identity is called a VALUE OBJECT.
* > VALUE OBJECTS can reference ENTITIES
* > When you care only about the attributes of an element of the model, classify it as a VALUE OBJECT. Make it express the meaning of the attributes it conveys and give it related functionality. Treat the VALUE OBJECT as immutable. Don't give it any identity and avoid the design complexities necessary to maintain ENTITIES.
* The attributes that make up a VALUE OBJECT should form a conceptual whole
# services
* > A SERVICE is an operation offered as an interface that stands alone in the model, without encapsulating state, as ENTITIES and VALUE OBJECTS do.
* A good SERVICE has three characteristics.
  * The operation relates to a domain concept that is not a natural part of an ENTITY or VALUE OBJECT.
  * The interface is defined in terms of other elements of the domain model.
  * The operation is stateless. Statelessness here means that any client can use any instance of a particular SERVICE without regard to the instance's individual history.
# modules
* there should be low coupling between MODULES and high cohesion within them
* 
