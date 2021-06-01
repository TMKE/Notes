## Looping through a list
The concept of looping is important because it's one of the most common ways a computer automates repetitive tasks.
```python
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(magician)
# Read this code as:
# "For every magician in the list of magicians"
```
>It's helpful to choose a meaningful name that represents a single item from the list.

Every indented line following the line `for magician in magicians` is considered _inside the loop_.
## Avoiding indentation errors
Python uses indentation to determine how a line, or group of lines, is related to the rest of the program.
```python
# These are some of the more common indentation errors
# 1. Forgetting to indent
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
print(magician)
"""
	File "magicians.py", line 3
		print(magician)
			^
IndentationError: expected an indented block
"""

# 2. Forgetting to indent additional lines
magicians = ['alice', 'david', 'carolina']
for magician in magicians:
	print(f"{magician.title()}, that was a great trick!")
print(f"I can't wait to see your next trick, {magician.title()}.\n")
# This is a logical error
# The syntax is valid Python code
# but doesn't produce the desired result

# 3. Indenting unnecessarily
message = "Hello Python world!"
	print(message)
"""
File "hello_world.py", line 2
	print(message)
	^
IndentationError: unexpected indent
"""

# 4. Indenting unnecessarily after the loop
for magician in magicians:
    print(f"{magician.title()}, that was a great trick!")
	print("Thank you everyone!")
# Python will consider the code inside the loop 
# but it's not the case in reality
# It's a logical error

# 5. Forgetting a colon
magicians = ['alice', 'david', 'carolina']
for magician in magicians 
	print(magician)
# This produces a syntax error
```
## Making numerical lists
### _Using the `range()` function_
```python
for value in range(1, 5):
	print(value)
# 1
# 2
# 3
# 4
```
`range()` only prints the numbers 1 through 4. This is another result of the _off-by-one_ behavior.
### _Using `range()` to make a list of numbers_
```python
numbers = list(range(1, 6))
print(numbers)
# [1, 2, 3, 4, 5]
```
If you pass a third argument to `range()`, Python uses that value as a step size when generating numbers.
```python
even_numbers = list(range(2, 11, 2))
print(even_numbers)
# [2, 4, 6, 8, 10]
```
_Example:_
```python
squares = []
for value in range(1, 11):
	squares.append(value ** 2)
print(squares)
# [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
### _Statistics_
```python
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
print(min(digits))
# 0
print(max(digits))
# 9
print(sum(digits))
# 45
```
### _List comprehensions_
The approach described earlier for generating the list `squares` consisted of using three or four lines. A _list comprehension_ allows you to generate this same list in just one line.
The _list comprehension_ combines the `for` loop and the creation of new elements into one line, and automatically appends each new element.
```python
squares = [value**2 for value in range(1, 11)]
print(squares)
```
## Working with part of a list
### _Slicing a list_
To make a slice, you specify the index of the first and last elements you want to work with.
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(players[0:3])
# ['charles', 'martina', 'michael']
```
>As with the `range()` function, Python stops one item before the second index specified.

If you omit the first/last index, Python automatically starts/ends at the beginning/end of the list.
```python
print(players[:4])
# ['charles', 'martina', 'michael', 'florence']

print(players[2:])
# ['michael', 'florence', 'eli']
```
This syntax allows you to output elements regardless of the length of the list.
```python
print(players[-3:])
# You can include a third value in the brackets.
# It tells Python how many items to skip between items in the specified range
print(players[0:4:2])
```
### _Looping through a slice_
```python
players = ['charles', 'martina', 'michael', 'florence', 'eli']
for player in players[:3]: 
	print(player.title())
"""
Charles 
Martina 
Michael
"""
```
### _Copying a list_
To copy a list, you can make a slice that includes the entire original list by omitting the indexes `[:]`.
```python
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods[:]
print(my_foods)
# ['pizza', 'falafel', 'carrot cake']
print(friend_foods)
# ['pizza', 'falafel', 'carrot cake']

my_foods.append('cannoli')
friend_foods.append('ice cream')
print(my_foods)
# ['pizza', 'falafel', 'carrot cake', 'cannoli']
print(friend_foods)
# ['pizza', 'falafel', 'carrot cake', 'ice cream']
```
If we had simply set `friend_foods` equal to `my_foods`, we would not produce two separate lists.
```python
my_foods = ['pizza', 'falafel', 'carrot cake']
friend_foods = my_foods

my_foods.append('cannoli') 
friend_foods.append('ice cream')

print(my_foods)
# ['pizza', 'falafel', 'carrot cake', 'cannoli', 'ice cream']
print(friend_foods)
# ['pizza', 'falafel', 'carrot cake', 'cannoli', 'ice cream']
```
This syntax tells Python to associate the `friend_foods` variable with the list that is already associated with `my_foods`, so now both variables point to the same list.
## Tuples
Tuples allow you to create a list of items that cannot change. Python refers to values that cannot change as immutable, and an immutable list is called a *tuple*.
### _Defining a tuple_
Once you define a tuple, you can access individual elements by using each item's index.
```python
dimensions = (200, 50)
print(dimensions[0]) 
# 200
print(dimensions[1])
# 50
```
If you try to change one of the items in the tuple, Python returns a type error.
```python
dimensions[0] = 250
```
Python tells us we can't assign a new value to an item in a tuple:
```
Traceback (most recent call last):
	File "dimensions.py", line 2, in <module>
		dimensions[0] = 250
TypeError: 'tuple' object does not support item assignment
```
>Tuples are technically defined by the presence of a comma; the parentheses make them look neater and more readable. If you want to define a tuple with one element, you need to include a trailing comma:
>```python
>my_t = (3,)
>```
>It doesn’t often make sense to build a tuple with one element, but this can happen when tuples are generated automatically.

### _Looping through all values in a tuple_
```python
dimensions = (200, 50) 
for dimension in dimensions: 
	print(dimension)
```
### _Writing over a tuple_
Although you can’t modify a tuple, you can assign a new value to a variable that represents a tuple:
```python
dimensions = (200, 50)
print("Original dimensions:")
for dimension in dimensions: 
	print(dimension)
"""
Original dimensions:
200
50
"""

dimensions = (400, 100)
print("Modified dimensions:")
for dimension in dimensions:
	print(dimension)
"""
Modified dimensions: 
400 
100
"""
```
## Styling your code
### _The style guide_
When someone wants to make a change to the Python language, they write a *Python Enhancement Proposal (PEP)*. One of the oldest PEPs is _PEP 8_, which instructs Python programmers on how to style their code.
### _Indentation_
PEP 8 recommends that you use four spaces per indentation level. Using four spaces improves readability while leaving room for multiple levels of indentation on each line.
>Every text editor provides a setting that lets you use the `TAB` key but converts each tab to a set number of spaces.

### _Line length_
Many Python programmers recommend that each line should be less than *80 characters*. Historically, this guideline developed because most computers could fit only 79 characters on a single line in a terminal window.
Using the standard line length allow you to see entire lines in two or three files that are open side by side onscreen. PEP 8 also recommends that you limit your comments to *72 characters per line*, because some of the tools that generate automatic documentation for larger projects add formatting characters at the beginning of each commented line.

### _Blank lines_
To group parts of your program visually, use blank lines (don't place three or four blank lines between the two sections).