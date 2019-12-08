# Notes about Python

## Object-Oriented Programming

It is a programming language model in which programs are organized around objects. An object is defined with attributes and methods. OOP focuses on the objects rather than the logic.

## Principles of OOP

Encapsulation - state of each object is privately held inside a class. Other objects do not have access or the authority to make changes. This data hiding provides greater program security and avoids unintended data corruption.

Abstraction - Objects only reveal internal mechanisms that are relevant for the use of other objects, hiding any unnecessary implementation code. This concept helps developers make changes and additions over time more easily.

Inheritance - Subclasses or children can inherit parent’s attributes and methods. This allows developers to reuse a common logic.

Polymorphism - Objects are allowed to take on more than one form depending on the context. The program will determine which meaning or usage is necessary for each execution of that object, cutting down on the need to duplicate code.

## Criticism of OOP

The largest concern is that OOP overemphasizes the data component of software development and does not focus enough on computation or algorithms. Additionally, the OOP code may be more complicated to write and take longer to compile.

## Procedure oriented programming

Old programming method. Top to bottom, giving instructions.

## Class / Instance

Instance is made with Class

## Private / Protected / Public

In python, no real private / protected attributes or methods
protected - single underscore
private - double underscore, it becomes \_classname\_\_ attributes / methods, have to access with public class method

## Class in python

```py
class CLASS:
	# CLASS.classAttribute
	classAttribute = value

	# constructor
	__init__(self, args):
		// instance attribute
		self.attribute = value

	# destructor
	__del__(self):

	# method override
	def parentMethod(self):
	# class parent method
	 super().parentMethod()

	# instance method
	def instanceMethod(self, args):
		return self.attribute

	# static method - no self parameter, can’t access instance attribute
	# CLASS.staticMethod / INSTANCE.staticMethod - both can be used
	@staticmethod
	def staticMethod(args):
		return something

	# class method, only access class attribute
  # can’t access instance attribute / method
  @classmethod
  def classMethod(cls, args):
	   return cls.classAttribute

  # operator overloading, __mul__, __len__, __getitem__, __str__
  def __add__(self, args):
	   return something

class = CLASS()
class.classAttribute
class.classMethod()

del class

# inheritance
class Children(Parent):
# multiple inheritance
class MultipleClass(Parent1, Parent2):

# check inheritance
issubclass(Children, Paren)
# check instance
isinstance(children, Children)

# abstract class
from abc import *

class Character(metaclass=ABCMeta):
  @abstractmethod
  def attack(self):
    pass
  @abstractmethod
  def move(self):
    pass
```

## id / is / ==

class = Class()
id(class) // return the address
is // same value and same instance
== // same value

## Problem with multiple inheritance

use super().**init**()
Order of calling parent’s method
You can find at CLASS.**mro**

## Composition OR Aggregation

When you want to use some of the methods of other class, try to avoid whole inheritance

```py
class Class:
	def __init__(self):
		self.OtherClass = OtherClass

	def otherMethod(self):
		return self.OtherClass.otherMethod()
```
