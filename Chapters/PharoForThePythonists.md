## Getting started

In this little book we will show that Pharo is easy to learn for a Pythonist.

- Dynamically typed
- REPL everywhere
- Objects everywhere

Pharo dynamic nature is close to the one of Python. 
Now Pharo is just uniform: the computation is expressed using only objects answering messages and lambas (lexical closure).

## Arithmetic

Let's start with basic messages for arithmetic operations.

#### Basic operators

```
1 + 2
>>> 3
```

```
1.1 * 2.3
>>> 2.53
```

Tips: in Pharo all the mathematic operators (`+`, '-', ...) can be defined on any class.

#### Power

```language=python	
4 ** 2
>>> 16 
```

In Pharo you can also use `raisedTo:` in addition to `**`.

```language=pharo
4 raisedTo: 2
>>> 16
```

#### Decimal and euclidean divisions

```
57/5
>>> 11.4 
```

```
57 // 5 
>>> 11
```

Tips: Use the example finder to discover the message based on the arguments. 

### Assignment

```language=python
x = 3
x = x + 2
x
```


```language=pharo
| x |
x :=  3
x := x + 2
x
>>> 5
```

`| x |` declares that we will use a temporary variable.
Note that the Playground declares automatically variable for you.


### Assigning multiple variables to the same value

```language=pharo
x := y := 3.
x + y
>>> 6
```

### Unsupported parallel assignment
Pharo does not support multiple assignments such as the following ones in Python. 

```language=python|unsupported
x, y = 6,4
```


### Special Pharo behavior

### Infinite numbers of digits


```language=pharo
(2 ** 90) numberOfDigits
>>28
```

```language=pharo
1 class
>>>SmallInteger
```

```language=pharo
1 class maxVal
>>xxx
```

Largest small integer
```language=pharo
(1 class maxVal) + 1
>>xxx
```

```language=pharo|test=true
((1 class maxVal) + 1) class
>> LargePositiveInteger
```

### No precedence

In Pharo arithmetic operations are plain messages. 
There is no precedence we should put parentheses to disambiguate.






### Questions: 
	how python is doing for x + y * z?

### Printing

####Internal console
```language=pharo
Transcript show: 'hello world'.
'Hello world' traceCr.
```
####External console
```language=pharo
STdio 'hello world'
```

### Input

We should do something here.

### Other numerical functions
Pharo offers a really large set of numerical functions. We will not list them all.

- abs
- int 
- mix
- max 
- round(x,n)

Tips: there is no variable number of argument in Pharo.

### Floats
 
- floor 
- sqrt
- cos, sin, tan
- atan, asin, acos

```lanuguage=pharo
arcTan
```

```
Float pi
```
Tips: Browse the class Float and SmallInteger

### Fractions

By default Pharo manipulates fractions. 
To create a fraction we use the message `/`.

```language=pharo|test=true
(1/3) + (2/3)
>>> 1
```

```language=pharo|test=true
(1/2) numerator
>>> 1
```

```language=pharo|test=no
testReciprocal
	self
		assert: (1 / 2) reciprocal equals: 2;
		assert: (3 / 4) reciprocal equals: 4 / 3;
		assert: (-1 / 3) reciprocal equals: -3;
		assert: (-3 / 5) reciprocal equals: -5 / 3
```

## Finder: a super powerful helper
Pharo offers a really nice set of powerful tool. 
The first one is the Finder. 

### Method names

### Class names

### Example-based methods


## Booleans and basic control flow 


### Booleans
In Pharo booleans `true` and `false` are instances of the class `True` and the class `False`.

```language=python
(1 > 3)
>>> False
```

```language=pharo
(1 > 3)
>>> false
```

```language=pharo
false class 
>>> False
```

### Boolean messages

#### Identity

```language=pharo
| x |
x := Object new.
x == x
>>> true
```

```language=pharo
Object new =~ Object new
>>> true
```

#### Comparison messages

Pharo offers default comparison messages: `<`, `>`, `>=`, `=`, `<=`. 

All subclasses of `Magnitude` are able to redefine such messages. 
  
#### Logic messages

```language=pharo
(1 < 5) & (5<10)
>>> true
```

```language=pharo
(5 < 1) and: [ 1/0 ]
>>> true
```

```language=pharo
5 between: 1 and: 10
>>> true
```

```language=pharo
(1 < 5) | false
>>> true
```
```language=pharo
(1 < 5) or: [ 1/ 0 ]
>>> true
```

### Simple conditions


Explanation: in Pharo there are only objects and messages. `ifTrue:`, `ifFalse:`, `ifTrue:ifFalse:`,.. are all messages sent to booleans

### if then

```language=python


```

```language=pharo
x ifTrue: [ ]

```

```language=pharo
x ifFalse: [ ]

```

### if then else

```language=python


```

```language=pharo
x 
	ifTrue: [ ]
	ifFalse: [ ]

```

```language=pharo
x 
	ifFalse: [ ]
	ifTrue: [ ]

```


## Characters, Strings and Symbols

In Pharo a string is a collection of `Character` instances. A string is delimited by a single quote. 
A symbol is a unique string.

```language=python
"hello world"
>>> "hello world"
```

```language=pharo
'hello world'
>>> 'hello world'
```

The class `String` defines a large number of methods. 

### Length of a string

Contrary to Python, in Pharo, getting the length of a string is just sending the message `size` to the string. 

```language=python
len("hello world")
>>> 11
```

```language=pharo
'hello world' size
>>> 11
```

### String concatenation
To concatenate two strings and get a new one, we send the message comma `,` to the first string.

The following example creates a string with all the alphabetic letters.

```language=python
x = ""
for i in range(97, 122):
	x = x+chr(i)
>>>xxx	
```

```language=pharo
| alpha |
alpha :=''.
(97 to: 122) do: [ :c | alpha := alpha, c asCharacter asString ].
alpha "'abcdefghijklmnopqrstuvwxyz'"
```

It is better to use a stream to avoid to create 26 strings that are then discarded. The Pharo idiomatic way is the following one: first we create a stream on a string and we place one by one the character using the `nextPut:` message.

```language=pharo
String streamContents: [ :st |
	(97 to: 122) do: [ :c | st nextPut: c asCharacter ]].
>>> 'abcdefghijklmnopqrstuvwxyz'
```

### Accessing
In Pharo the first element of a string starts at index 1 and we can access element using the message `at:`.

```language=pharo
'Pharo is c00l' at: 5
>>> $o
```


```language=python
st = "Pharo is cool"
for i in range(0, len(st):
	print("Char :, i, st[i])
>>>	
```

A first variation using `at:`.
```language=pharo
| st |
st := 'Pharo is cool'.
1 to: st size do: [ :i | 
	st traceCr: ('Char {1} is {2}.' format: { i . st at: i }) ]
```

A second variation using `withIndexDo:`.
```language=pharo
| st |
st := 'Pharo is cool'.
st withIndexDo: [ :c :i | 
	st traceCr: ('Char {1} is {2}.' format: { i . c  }) ]
```

```language=pharo
Char 1 is P.
Char 2 is h.
Char 3 is a.
Char 4 is r.
Char 5 is o.
Char 6 is  .
Char 7 is i.
Char 8 is s.
Char 9 is  .
Char 10 is c.
Char 11 is o.
Char 12 is o.
Char 13 is l.
```

### Some other string messages

```language=pharo
'Pharo is c00l' allButFirst: 6 
>>>'is c00l'
```

```language=pharo
'Pharo is c00l' copyFrom: 11 to: 12  
>>> '00'
```

## Some loops

Pharo offers many different loops and conditional loops. Such loops can be traditional loops using explicit index access or iterators. 

### Explicit iteration

#### to:do: and to:do:by:

```language=pharo 
1 to: 100 by: 3 do: [:i | i traceCr]
```

```language=pharo 
1 to: 100 by: 3 do: [:i | i traceCr]
```

```language=python 
for i in range(1,6):
	print(i)
```

```language=pharo 
1 to: 6 do: [ :i | i traceCr ]
```


When you have an expression to execute a number of times, you can also use the message `timesRepeat:` as follows: 
```
6 timesRepeat: [ 1 traceCr ]
```

#### With an iterator
```language=pharo 
(1 to: 6) do: [ :i | i traceCr ]
```


## Conditional iteration


```language=python
end = 10
count = 1
while count <= end
	print("A")
	count = count + 1
print("end")
```

```language=pharo
| end count |
end := 10.
count := 1. 
[ count <= end ] whileTrue: 
	[ 'A' traceCr.
	count := count + 1
	]
```

```
[] whileFalse: []
```

## Methods

Pharo is a pure object-oriented language. 
You can only define methods in a class.
Methods can simply return a value (and be similar to functions) or change the state of the object to which they are applied. 
By default a method returns the receiver of the message. 

### Example

Imagine that we would like to compute the body mass index defined as the quotient of the height by the square of the weigth.

```language=python
def bodyMassIndex(height, weigth)
	return int(round(weigth / height** 2),0)
```

In Pharo we will define a class named `Calculator`

```language=pharo
Object << Calculator
	package: 'Pyt'
	
bodyMaxIndexFor: height and: weigth
	^ ((weigth / (height * height)) rounded
```

The character `^` is the method return expression.


### Lambdas

Pharo also offers lexical closure named lambda in Python. A lexical closure in Pharo is like an anonymous method which is not defined in a class.

Closures are central to Pharo, most of the control flow mechanism such as conditionals, loops, and iterators are based on closures. 

```language=python
f=lambda x : -x + 4
f(3)
>>> 1
```

In Pharo closures are objects that are executed sending them the messages `value:`.


```language=pharo
f := [:x | -x + 4].
f value: 3
>>> 1
```


```language=pharo
g := [:x :y| -x + y].
g value: 3 value: 4
>>> 1
```






## First data structures

Pharo defines many different data structures such as `Set`, `Array`, `OrderedCollection`, `Dictionary`, `Bag`, `LinkedList`, ... 
We will start by an overview of the common data structure objects.
Then we will show how Python lists are close to Pharo's ordered collections.

## Basic mapping
Python offers tuples, lists, dictionaries, and arrays.
Pharo proposes nearly the same with some difference we briefly sketch now. 

- Python lists - Pharo ordered collections. `OrderedCollection`'s are growable data structures where elements can be freely added, inserted or removed. `OrderedCollection`s are similar to `LinkedList` which support better insertion at the cost of wrapping the value in cells.

- Python tuples - Pharo pairs. Pharo does not have immutable pairs as in Python. It offers simple mutable pairs. Such pair only works with two elements (a key and value) and are not supported to values in multiple variables.

- Python arrays - Pharo arrays. Arrays in Pharo are similar to the ones in Python. They are fixed size arrays. They can hold any objects. Pharo offers different ways to express arrays: literal arrays (using `#( a)` ) are parse time arrays which will first only contain literal objects (true, nil, string, numbers, arrays), dynamically-created arrays 
(using `{ 1 + 2 . 3+3 }` an array of two elements 3 and 6) which can initially contain any objects.

- Python dictionaries - Pharo dictionaries. A Pharo `Dictionary` is growable key value data structure. Several variations exists whether we want to compare based on equality or identity.

In addition Pharo supports many other data structures. The most common ones being `Set`, `Bag`, 

### List / OrderedCollection

```
x=[10,12,12,12,13,14,14,15]
x.count(12)
>>> 3
```

Ordered collection instances can hold really large amount of objects. For example in the Moose reengineering platform it is frequent to hold more than 600,000 objects. 

Now in script creating ordered collections is verbose so we will convert arrays as ordered collection.
The main difference between Array and OrderedCollection is that Array have fixed size and cannot grow dynamically. 

```language=python
x=[10,12,12,12,13,14,14,15]
x.count(12)
>>> 3
```

```language=pharo
x := #(10 12 12 12 13 14 14 15) asOrderedCollection.
x occurrencesOf: 12
>>> 3
```

Pharo does not propose predefined ways to create lists based on range but we can create intervals which are object representing range.

```language=python
pair=range(0,20,2)
```

```language=pharo
pair=(0 to: 20 by: 2)
```

Another way is to convert an interval into an ordered collection.

```language=pharo
pair=(0 to: 20 by: 2) asOrderedCollection
```
Here is an explicit way to create an OrderedCollection with all the multiples of 7 and 9 from 0 to 10000. 
This way can be easily generalized

```
| col |
col := OrderedCollection new. 
0 to: 10000 do: [ :each |
	(each rem: 7) isZero 
		and: [ (each rem: 9) isZero ifTrue: [ col add: each ] ] ].
col
```

The following program builds a new list (in fact it builds many intermediate lists). 

```language=python
pair = []
for i in range(0,20,2):
	pair=pair+[i]
```

An equivalent growing the original collection is 

```language=python
pair := OrderedCollection new.
(0 to: 20 by: 2) do: [ :el |
	pair add: el ]
```

Pharo's OrderedCollection offers a large API. For example here are all the methods for just the addition of an element: 

- `addAllFirstUnlessAlreadyPresent:` 
- `add:after:` 
- `add:afterIndex:` 
- `add:beforeIndex:` 
- `addFirst:` 
- `add:` 
- `addAllFirst:` 
- `addLast:` 
- `add:before:` 
- `addAll:`
- `addAllLast:`

The following script generates the list taking into account locally defined methods of the class `OrderedCollection`.

`OrderedCollection` offers way to insert, delete, reverse, sort, and verify various predicates.









