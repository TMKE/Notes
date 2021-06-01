## Working with dictionaries
A *dictionary* in Python is a collection of *key-value* pairs. You can use a key to access the value (it could be a number, a string, a list, a dictionary or any object) associated with that key.
```python
alien_0 = {'color': 'green', 'points': 5}
print(alien_0['color'])
# green
print(alien_0['points'])
# 5
```
#### *Adding new key-value pairs*
Dictionaries are dynamic structures, and you can add new key-value pairs at any time.
```python
alien_0 = {'color': 'green', 'points': 5}
alien_0['x_position'] = 0
alien_0['y_position'] = 25
print(alien_0)
# {'color': 'green', 'points': 5, 'y_position': 25, 'x_position': 0}
```
#### *Starting with an empty dictionary*
It's sometimes convenient, or even necessary, to start with an empty dictionary then add items to it.
```python
alien_0 = {}
```
#### *Modifying values in a dictionary*
```python
alien_0 = {'color': 'green'}
alien_0['color'] = 'yellow'
```
#### *Removing key-value pairs*
```python
alien_0 = {'color': 'green', 'points': 5}
del alien_0['color']
```
#### *A dictionary of similar objects*
You can use a dictionary to store one kind of information about many objects.
```python
favorite_languages = { 
	'jen': 'python', 
	'sarah': 'c',
	'edward': 'ruby',
	'phil': 'python', 
	}
```
#### *Using `get()` to access values*
Using keys might cause potential probelm: if the key you ask for doesn't exist, you'll get an error.
```python
alien_0 = {'color': 'green', 'speed': 'slow'}
print(alien_0['points'])
```
```
Traceback (most recent call last):
	File "alien_no_points.py", line 2, in <module>
		print(alien_0['points']) 
KeyError: 'points'
```
The `get()` method sets a default value to be returned if the requested key doesn't exist.
The `get()` method requires a key as a first argument. As a second optional argument, you can pass the value to be returned if the key doesn't exist:
```python
alien_0 = {'color': 'green', 'speed': 'slow'}

point_value = alien_0.get('points', 'No point value assigned.') 
print(point_value)
# No point value assigned.
```
>If you leave out the second argument and the key doesn't exist, Python will return the value `none`.

## Looping through a dictionary
#### *Looping through key-value pairs*
```python
user_0 = {
	'username': 'efermi',
	'first': 'enrico',
	'last': 'fermi',
	}
	
for key, value in user_0.items():
	print(f"\nKey: {key}")
	print(f"Value: {value}")
```
The `items()` method returns a list of key-value pairs.
#### *Looping through keys*
```python
favorite_languages = { 
	'jen': 'python', 
	'sarah': 'c', 
	'edward': 'ruby', 
	'phil': 'python',
	}
	
for name in favorite_languages.keys():
	print(name.title())
```
Looping through all keys is actually the default behavior when looping through a dictionary, so this code would have exactly the same output if you wrote:
```python
for name in favorite_languages:
```
The `keys()` method isn't just for looping: it actually returns a list of all the keys.
#### *Looping through keys in a particular order*
You can use the `sorted()` function to get a copy of the keys in order:
```python
favorite_languages = { 
	'jen': 'python', 
	'sarah': 'c', 
	'edward': 'ruby', 
	'phil': 'python',
	}

for name in sorted(favorite_languages.keys()):
	print(f"{name.title()}, thank you for taking the poll.")
# Edward, thank you for taking the poll.
# Jen, thank you for taking the poll.
# Phil, thank you for taking the poll.
# Sarah, thank you for taking the poll.
```
#### *Looping through values*
```python
for language in favorite_languages.value():
	print(language.title())
```
This approach pulls all the values from a dictionary without checking for repeats. This might work fine with a small number of values, but with a large number, this would result in a very repetitive list.
To see each language chosen without repetition, we can use a set.
A *set* is a collection in which items must be unique:
```python
for language in set(favorite_languages.values()):
	print(language.title())
```
>You can build a set directly:
>```python
>languages = {'python', 'ruby', 'python', 'c'}
>```
>Unlike lists and dictionaries, sets do not retain items in any specific order.

## Nesting
You can nest dictionaries inside a list, a list inside a dictionary, or even a dictionary inside another dictionary.
#### *A list of dictionaries*
```python
# Make an empty list for storing aliens
aliens = []

# Make 30 green aliens
for i in range(30)
	new_alien = {'color': 'green', 'points': 5, 'speed': 'slow'}
	aliens.append(new_alien)

# Show how many aliens have been created
print(f"Total number of aliens: {len(aliens)}")
```
#### *A list in a dictionary*
If you want more than one value to be associated with a single key, you can nest a list inside a dictionary.
```python
pizza = {
	'crust': 'thick',
	'toppings': ['mushrooms', 'extra cheese'],
	}
```
>You shouldn't nest lists and dictionaries too deeply, because most likely a simpler way to solve the problem exists.

#### *A dictionary in a dictionary*
*Example:* If you have several users for a website, each with a unique username, you can use the usernames as keys. You can store information about each user by using a dictionary as the values associated with their usernames.

```python
users = {
	'aeinstein': {
		'first': 'albert',
		'last': 'einstein',
		'location': 'princeton',
		},
	'mcurie': {
		'first': 'marie',
		'last': 'curie',
		'location': 'paris',
		},
	}
```
Notice that the structure of each user's dictionary is identical. Although not required by Python, this structure makes nested dictionaries easier to work with.