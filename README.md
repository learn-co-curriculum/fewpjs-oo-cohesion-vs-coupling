# Cohesion and Coupling

## Learning Goals

- Understand the meaning of cohesion in regards to OO design
- Understand the meaning of coupling in regards to OO design
- Recognize the value of having high cohesion and weak coupling

## Introduction

When we talk about the _design_ of Object Oriented applications, our main goalis
to make our applications flexible to change and easy to understand. By doing so,
our applications will be easier to maintain and extend over time. While we are
free to design classes and their interactions however we please, some designs
_are_ more flexible and easier to understand than others.

So how do we approach designing such an application? What **_is_** a good design
pattern to follow?

We've already touched on the single responsibility principle, and we will touch
on a few more in upcoming lessons, but before we can understand the value of
these principles, we need to understand two terms: **cohesion** and
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

To maintain high cohesion, the best practice is to simply follow the single responsibility principle. **The single responsibility principle tends to create highly cohesive classes automatically by encouraging us to stick to small, simple class designs.**

## Coupling

Coupling is an abstract measure of _how dependent_ classes are to each other. To
say two or more classes are strongly coupled means that they are highly dependent
on each other. Weak coupling, on the other hand, means that classes are minimally dependent on each other.

Every dependency we establish strengthens coupling, but remember that each
dependency is established in one direction. So,
for instance, class A might be dependent on class
B, but not the other way around. Class A is weakly coupled to class B. We can represent this
dependency visually:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/dependency.png" width=400px />

If class A is given additional dependencies on class B, it becomes more dependent and thus, more strongly coupled.

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/high_coupling.png" width=400px />

Many classes can also be strongly coupled together. Consider the following visual example:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/high_coupling_many_classes.png" width=400px />

Each arrow represents a dependency. It _may be argued_ that we need all of these
connections for our particular application, but we pay a price. Classes B, C and
D, for instance, are all dependent on class E. If you change something in class
E, say the _name_ of a property, it could have an impact on at least three other
classes, more if any classes are dependent on E _through_ classes B, C, or D.

On the other hand, consider the following:

<img src="https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-cohesion-and-coupling/low_coupling_many_classes.png" width=400px />

Given the above dependencies, if we needed to change class E, class C will not
be affected by any changes made. We've decoupled the two and weakened coupling
elsewhere.

**Note:** One thing not shown in the images above is that its also possible to
establish a dependency between classes _through_ one or more classes in between.
Class D is dependent on class E, but classes A and B _might_ also be, _through_
class D.

Its important to keep in mind - _more_ **total** dependencies **does not mean
stronger coupling**. Dependencies are a necessary part of class based design.
The key is that classes should have fewer dependencies between each other. Four
classes, each with one dependency on another has weaker coupling than two
classes with four dependencies between them.

Strongly coupled classes tend to make our code less flexible to modification, as
one change might require significant rewriting of multiple classes if we ever
want to update or extend them.

There are some additional principles we can use to maintain weak coupling in our
applications that we will discuss in upcoming lessons. In general though, the key things to remember to keep your coupling from getting too strong:

#### Follow SRP

Follow the single responsibility principle to maintain high cohesion. If
a class only has _one_ responsibility, it will be **minimally** dependent on
other classes. At the same time, a minimal number of classes will dependent on
it.

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

By trying to keep dependencies between close neighbors, this can be avoided.
Typically, class A should not need to know about classes C and D - its the
responsibility of class B to know about C and D. If you find you need to use
class E from class A, there may also be a different configuration of
dependencies that is better for your application.

## Conclusion

The great thing about cohesion and coupling is that they go hand in hand. High
cohesion by definition tends to lead to weak coupling. Classes that do many
things tend to be depended on more by other classes.

Every Object Oriented application requires the use of dependencies between
classes or objects, but the _more_ interdependent classes are the harder it is
to understand and maintain.

## Resources

- [Cohesion]: https://en.wikipedia.org/wiki/Cohesion_(computer_science)

[solid]: https://en.wikipedia.org/wiki/SOLID
