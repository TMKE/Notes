## What's a list?
A *list* is a *collection of items* (letters, digits, names et.) in *particular order*. _Those items don't have to be related in any particular view_.
>It's a good idea to make the name of your list plural, such as `letters`, `digits`, or `names`.
```python
bicycles = ['trek', 'cannaondale', 'redline', 'specialized']
print(bicycles)
# ['trek', 'cannondale', 'redline', 'specialized']
# Python returns its representation of the list
```
### ***Accessing elements in a list***
You can access any element in a list by telling Python its position (_index_).
```python
print(bicycles[0].title())
```
### _*Index positions start at 0, not 1*_
This is true of most programming languages, and the reason has to do with how the list operations are implemented at a lower level.
>Python has a special syntax for accessing the last element in a list:
>```python
>print(bicycles[-1])
># specialized
>```
>This is useful because you don't have to know the size of the list. This convention extends to other negative index values as well, like `-2` and `-3`.
### _*Using individual values form a list*_
```python
message = f"My first bike was a {bicycles[0].title()}."
print(message)
```
## Changing, adding, and removing elements
Most lists you create will be _dynamic_.
### _*Modifying elements in a list*_
```python
motorcycles = ['honda', 'yamaha', 'suzuki'] 
print(motorcycles)
# ['honda', 'yamaha', 'suzuki']
motorcycles[0] = 'ducati' 
print(motorcycles)
# ['ducati', 'yamaha', 'suzuki']
```
### _*Adding elements to a list*_
#### *Appending elements to the end*

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.append('ducati')
print(motorcycles)
# ['honda', 'yamaha', 'suzuki', 'ducati']
```
#### _Inserting elements_ (at a given position)

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.insert(0, 'ducati') 
print(motorcycles)
# ['ducati', 'honda', 'yamaha', 'suzuki']
```
### *_Removing elements_*
#### _Using the `del` statement_
This is used when we know the position of the item we want to remove.

```python
motorcycles = ['honda', 'yamaha', 'suzuki'] 
print(motorcycles)
# ['honda', 'yamaha', 'suzuki']
del motorcycles[0] 
print(motorcycles)
# ['yamaha', 'suzuki']
```
#### _Using the `pop()` method_
The `pop()` method removes the last item in a list and returns its value.

> The term _pop_ comes from thinking of a list as a stack and popping one item off the top of the stack.
```python
motorcycles = ['honda', 'yamaha', 'suzuki'] 
print(motorcycles)
# ['honda', 'yamaha', 'suzuki']

popped_motorcycle = motorcycles.pop()
print(motorcycles)
# ['honda', 'yamaha']
print(popped_motorcycle)
# suzuki
```
#### _Popping items from any position_
You can use `pop(index)` to remove the item at the index `index`.

```python
motorcycles = ['honda', 'yamaha', 'suzuki']
first_owned = motorcycles.pop(0)
print(f"The first motorcycle I owned was a {first_owned.title()}.")
# The first motorcycle I owned was a Honda.
```
#### _Removing items by value_
If you know the value you want to remove, you can use the `remove()` method.

```python
motorcycles = ['honda', 'yamaha', 'suzuki', 'ducati']
print(motorcycles)
# ['honda', 'yamaha', 'suzuki', 'ducati']

motorcycles.remove('ducati')
print(motorcycles)
# ['honda', 'yamaha', 'suzuki']
```
>The `remove()` method deletes only the first occurrence of the value you specify.
## Organizing a list
### _*Sorting a list permanently with `sort()` method*_
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort()
print(cars)
# ['audi', 'bmw', 'subaru', 'toyota']
```
We can also sort in reverse alphabetical order by passing the argument `revers=True` to the `sort()` method.
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort(reverse=True)
print(cars)
# ['toyota', 'subaru', 'bmw', 'audi']
```
### *Sorting a list temporarily with `sorted()` method*
The `sorted()` function lets you display your list in a particular order by doesn't affect the actual order of the list.
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(cars)
# ['bmw', 'audi', 'toyota', 'subaru']

print(sorted(cars))
# ['audi', 'bmw', 'subaru', 'toyota']

print(cars)
# ['bmw', 'audi', 'toyota', 'subaru']
```
The `sorted()` function can also accept a `reverse=True` argument `print(sorted(cars, reverse=True))`.
### _Reversing a list_
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.reverse()
print(cars)
# ['subaru', 'toyota', 'audi', 'bmw']
```
### _Finding the length of a list_
```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
print(len(cars))
# 4
```
## Avoiding index errors
```python
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles[3])
"""
Traceback (most recent call last):
	File "motorcycles.py", line 2, in <module>
		print(motorcycles[3])
IndexError: list index out of range
"""
```
Python attempts to give you the item at index 3, but no item has an index of 3. Because of the _off-by-one_ nature of indexing in a list, this error is typical.