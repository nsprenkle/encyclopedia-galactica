# SOLID Design Principles

## Single Responsibility

A class or function should do only one thing and do it well.

A classic code smell for this is the word `and` in any signature

## Open / Closed

## Liskov Substitution (Hanks / Cage Substitution)
Classes should be substitutable for their base classes

## Interface Segregation
  - If there's a class with members A-Z and you need only need access to A & B, create a new interface which has A & B, and an interface with C-Z which inherits from the previous interface. This allows interface 1 to not be fat, and allows interface 2 to be used in place of an original class.
  - Look for unimplemented interface / class methods, or client which references only a small portion of a class

## Dependency Inversion Principle

  - Constructor injection, dependencies are passed in via constructor
  - Property/setter injection, dependencies are properties set after constructor
  - Parameter injection, dependencies passed in as parameters per function
