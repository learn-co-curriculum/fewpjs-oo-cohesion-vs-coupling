# Cohesion and Coupling

## Learning Goals

- Understand the meaning of cohesion in regards to OO design
- Understand the meaning of coupling in regards to OO design
- Recognize the value of having high cohesion and weak coupling

## Introduction

When we talk about the _design_ of Object Oriented applications, our main goal
is to make our applications flexible to change and easy to understand. By doing
so, our applications will be easier to maintain and extend over time. While we
are free to design classes and their interactions however we please, some
designs _are_ more flexible and easier to understand than others.

So how do we approach designing such an application? What **_is_** a good design
pattern to follow?

We've already touched on the single responsibility principle, and we will touch
on a few more principles in upcoming lessons. Before we can understand the
value of these principles, we need to understand two terms: **cohesion** and
**coupling**.

In this lesson, we're going to talk a bit about cohesion and coupling and how we
use them when considering the design of an Object Oriented application. In
short, though, the main thing to keep in mind as we go through this lesson:

**Good software design has high cohesion and weak coupling.**

## Cohesion

Cohesion is an abstract measure of _how related_ elements are inside a class.
To say a class has _high_ cohesion in JavaScript means that the properties
and methods of the class are all closely related. Highly cohesive classes tend
to be simpler and easier to understand.

_Low_ cohesion, on the other hand, means a class' information and behaviors are
broad. It has many responsibilities. If a class is doing ten different things,
it is much harder to understand its purpose and how those things are all
connected.

To maintain high cohesion, the best practice is to simply follow the single
responsibility principle. **The single responsibility principle tends to create
highly cohesive classes automatically by encouraging us to stick to small,
simple class designs.**

## Coupling

Coupling is an abstract measure of _how dependent_ classes are to each other. To
say two or more classes are strongly coupled means that they are highly
dependent on each other. Weak coupling, on the other hand, means that classes
are minimally dependent on each other.

Every dependency we establish strengthens coupling, but remember that each
dependency is established in one direction. So, for instance, class A might be
dependent on class B, but not the other way around. Class A is weakly coupled to
class B. We can represent this dependency visually:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/dependency.png" width=400px />

If class A is given additional dependencies on class B (for instance, if class A
relied on _many_ properties from class B), it becomes more dependent and thus,
more strongly coupled.

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/high_coupling.png" width=400px />

The measure of coupling also applies to groups of many classes, which can also
be strongly coupled together. Consider the following visual example:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/high_coupling_many_classes.png" width=400px />

Each arrow represents a dependency. It _may be argued_ that we need all of these
connections for our particular application, but we pay a price. Classes B, C and
D, for instance, are all dependent on class E. If you change something in class
E, say the _name_ of a property, it could have an impact on at least three other
classes. The more dependencies we establish, the stronger the coupling. Strongly
coupled classes become inflexible. Changing one class may require changing many
other dependent classes.

**Note:** This diagram doesn't display it, but there may actually be additional
classes that are dependent on E _through_ classes B, C, or D. Class A, for
instance, might include a method that accesses a property on class E _through_
class B.

On the other hand, consider the following:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/low_coupling_many_classes.png" width=400px />

Given the above dependencies, if we needed to change class E, class C will not
be affected by any changes made. Changing a property in class E might require
some changes in class D. While it is possible for classes A and B to still be
dependent on class E (through D), there is now only _one_ route for A and B to
couple with E. The amount of dependencies is kept to near a minimum, making it
less expensive to make any changes later on.

In terms of code, this class structure may look fundamentally different than it
did when we had stronger coupling. However, we still have enough dependencies
that we can _get_ to all the classes and their properties and methods.

This example simplifies the concept of coupling a bit. Its important to keep in
mind - _more_ **total** dependencies **does not mean stronger coupling**.
Dependencies are a necessary part of class based design. The key is that classes
should have fewer dependencies between each other. Four classes, each with one
dependency on another has weaker coupling than two classes with four
dependencies between them.

Strongly coupled classes tend to make our code less flexible to modification, as
one change might require significant rewriting of multiple classes if we ever
want to update or extend them. Strong coupling also often results in more
'bespoke' code. That is, customized code used for defining a specific
relationship. The less bespoke code we use, the more our components become
reusable.

De-coupling existing code can be difficult, and often require additional classes
to separate out some of the dependencies (something we will look at in upcoming
lessons).

The important thing, then, is to keep coupling in mind from the very. When
you're designing an application's classes, these are the key things to remember
to keep your coupling from getting too strong:

#### Follow SRP

Follow the single responsibility principle to maintain high cohesion. If a class
only has _one_ responsibility, it will be **minimally** dependent on other
classes. Applying this accross the board encourages us to create _more_ classes
with _fewer_ dependencies, maintaining weaker coupling.

#### Keep Dependencies between Close Neighbors

Because dependencies tend to form chains, it is possible for the first class
in a chain of dependencies to have access to many other classes:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/low_coupling_many_classes.png" width=400px />

Class A in this example is dependent on class B. It has access to all of class
B's properties and methods. Since class B is dependent on classes C and D, A
also has the ability to access classes C and D. Again, since class A can access
class D, it can also access class E. This means that we _could_ write a
method in class A that establishes a dependency on C, D or E, strengthening
coupling between these classes.

Sometimes this might be necessary. It may be that these five classes form a
larger 'organ' in our application, a related group - they might be intrinsically
tied together, with class A being the 'interface' for other parts of the
application to access this 'organ.'

This is fine if necessary. In general, though, when one class is dependent on
another through a third class (and/or fourth, fifth, sixth, etc..) it is good
to ask - _can_ one of the intermediate classes handle this dependency instead?

Class A might initially seem like it needs to be dependent on class E, but if
there is a way for class B, or even better, class D, to handle the dependency,
our classes wont be so strongly coupled. This might allow for class A to become
more generic or abstract without changing the overall functionality of the app.

## Conclusion

Every Object Oriented application requires the use of dependencies between
classes or objects, but the _more_ interdependent classes are the harder it is
to understand and maintain. Cohesion and coupling are measurements we can use
to help guide us in the process of writing well designed Object Oriented code.

The great thing about cohesion and coupling is that they go hand in hand. High
cohesion by definition tends to lead to weak coupling. A class that does many
things has low cohesion, and because it does so much, there is a greater likelihood that many other classes depend on it, leading to stronger coupling.

## Resources

- [Cohesion][cohesion]
- [Coupling][coupling]

[cohesion]: https://en.wikipedia.org/wiki/Cohesion_(computer_science)
[coupling]: https://en.wikipedia.org/wiki/Coupling_(computer_programming)
[solid]: https://en.wikipedia.org/wiki/SOLID
