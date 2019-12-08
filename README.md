# Notes about Python

[Object-Oriented Programming](#-OOP)

[Data Structure and Algorithm](#-Data-Structure)

[Sorting](#-Sorting)

# OOP

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

## When you build class

S - SRR(Single Responsibility Principle)

O - OCP(Open Closed Principle), open for extension but closed for change

L - LSP(Liskov Substitusion Principle), parent / child can be substituted

I - ISP(Interface Segregation Principle), if method is not related or useless, it should be separated

D - DIP(Dependency Inversion Principle) - Parent should not depend on Children

## Design pattern

### Singleton pattern

Single instance per class

```py
class CLASS(metaclass=Singleton):
```

### Observer pattern

when attributes change, notify all related objects

### Builder pattern

provide SOME of args, set default values

### Factory pattern

factory class making objects

## namedtuple

### collections.namedtuple

class with only attributes

```py
import collections
Employee = collections.namedtuple('Employee', ['name', 'id'])
# or Employee = collections.namedtuple('Person', 'name, id')
employee1 = Employee('Dave', '4011')
```

### typing.NamedTuple

```py
from typing import NamedTuple

class Employee(NamedTuple):
    name: str
    id: int

employee1 = Employee('Guido', 2)
```

# Data Structure

## Time complexity / Space complexity (memory)

Big O notation O(N)

Ω omega notation Ω(N) - best running Time

Θ theta notation Θ(N) - average running Time

O(1) < O(logn) < O(n) < O(nlogn) < O(n2) < O(2n) < O(n!)

## Array

pro: fast access

con: add / remove is hard

## Queue

```py
import queue
# first in, first out
data_queue = queue.Queue()
data_queue.put('first')
data_queue.qsize()
data_queue.get()
# last in first out
data_queue = queue.LifoQueue()
# priority queue
data_queue = queue.PriorityQueue()
# low rank, first out
data_queue.put((10, 'first'))
```

## Stack

First in, last out

pro: easy to implement, fast read/write

con: set max number of stack, max 1000 recursive function, possible memory leak

simply use, list append and pop

## Linked List

```py
class Node:
    def __init__(self, data, next=None):
        self.data = data
        self.next = ''
```

pro: no need to set size

con: not good storage efficiency, slow access, delete middle needs additional work

### Doubly linked list

```py
class Node:
    def __init__(self, data, prev=None, next=None):
        self.prev = prev
        self.data = data
        self.next = next
```

## Hash Table

key, value pair - Use Dictionary

Hash - change value to fixed length value

Hashing Function - translate key to address

Use when searching needs a lot

pro: fast write / read, easy to find duplicate

con: require more space, need a function to avoid duplications

```py
# hashing function
hash('Dave')
```

### Hash Collision resolutions

- Chaining
- Linear Probing

### Hash table complexity

Collision: Average O(1), worst O(n)

Search: O(1)

## Tree

### Binary Search Tree

![alt text](https://github.com/dmrg2/pythonNote/blob/master/tree.png)

![alt text](https://github.com/dmrg2/pythonNote/blob/master/binarySearch.gif)

```py
class Node:
    def __init__(self, value):
        self.value = value
        self.left, self.right = None, None

class NodeMgmt:
    def __init__(self, head):
        self.head = head

    def insert(self, value):
        self.current_node = self.head
        while True:
            if value < self.current_node.value:
                if self.current_node.left != None:
                    self.current_node = self.current_node.left
                else:
                    self.current_node.left = Node(value)
                    break
            else:
                if self.current_node.right != None:
                    self.current_node = self.current_node.right
                else:
                    self.current_node.right = Node(value)
                    break

    def search(self, value):
        self.current_node = self.head
        while self.current_node:
            if self.current_node.value == value:
                return True
            elif value < self.current_node.value:
                self.current_node = self.current_node.left
            else:
                self.current_node = self.current_node.right
        return False
```

### Time complexity

depth = h

h = log2n, so O(log n), worst O(n)

## Heap

easy to find min / max - takes O(logn)

## Space complexity

## Recursive Call

# Sorting

## Selection Sort

```py
# python's sorted uses selections sort
sorted(data_list)
```

1. Find minimum value
2. Swap with the first one
3. Do 1 and 2 for the rest

```py
def selection_sort(data_list):
    for index in range(len(data_list) - 1):
        lowest = index
        for index2 in range(index + 1, len(data_list)):
            if data_list[lowest] > data_list[index2]:
                lowest = index2
        data_list[index], data_list[lowest] = data_list[lowest], data_list[index]
    return data_list
```

As you can see, O(n2)

## Insertion Sort
