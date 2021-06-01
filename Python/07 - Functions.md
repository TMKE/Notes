*Functions* are named blocks of code that are designed to do one specific job.
## Defining a function
```python
def greet_user():
	"""Dispaly a simple greeting."""
	print("Hello!")

greet_user()
```
* `def` keyword informs Python that you're defining a function. This is the *function definition*, which tells Python the name of the function and, if applicable, what kind of information the function needs to do its job.
* The indented lines make up the body of the function.
* The text `"""Dispaly a simple greeting."""` is a comment called *docstring*, which describes what the function does. Python looks for docstrings when generating documentation for the functions in your programs.
* To use a function, you call it.
#### *Passing information to a function*
```python
def greet_user(username):
	"""Dispaly a simple greeting."""
	print(f"Hello {username.title()}!")

greet_user('djamel')
# Hello Djamel!
```
#### *Arguments and parameters*
The variable `username` in the definition of `greet_user()` is a *parameter*, a piece of information the function needs to do its job. The value `djamel` in `greet_user('djamel')` is an *argument*, a piece of information that's passed from a function call to a function.
## Passing arguments
#### *Positional arguments*
Python must match each argument in the function call with a parameter in the function definition (order matters in positional arguments).
```python
def describe_pet(animal_type, pet_name):
	"""Display information about a pet.""" 
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")
	
describe_pet('hamster', 'harry')
```
#### *Keyword arguments*
A *keyword argument* is a name-value pair that you pass to a function. You explicitly tell Python which parameter each argument should be matched with.
```python
describe_pet(animal_type='hamster', pet_name='harry')
```
#### *Default values*
You can define a *default value* for each parameter, which will be used when no argument for a parameter is provided in the function call.
```python
def describe_pet(animal_type='hamster', pet_name):
	"""Display information about a pet.""" 
	print(f"\nI have a {animal_type}.")
	print(f"My {animal_type}'s name is {pet_name.title()}.")
	
describe_pet(pet_name='harry')
```
>When you use default values, any parameter with a default value needs to be listed after all the parameters that don’t have default values. This allows Python to continue interpreting positional arguments correctly.

>You can combine between the three methods

#### *Avoiding argument errors*
```python
describe_pet()
```
```
Traceback (most recent call last):
	File "pets.py", line 6, in <module>
		describe_pet()
TypeError: describe_pet() missing 2 required positional arguments: 'animal_ type' and 'pet_name'		
```
Python is helpful in that it reads the function's code for us and tells us the names of the arguments we need to provide.
## Return values
The value the function returns is called a *return value*.
#### *Returning a simple value*
```python
def get_formatted_name(first_name, last_name):
	"""Return a full name, neatly formatted."""
	full_name = f"{first_name} {last_name}"
	return full_name.title()
	
print(get_formatted_name('jimi', 'hendrix'))
```
#### *Making an argument optional*
You can use default values to make an argument optional.
```python
def get_formatted_name(first_name, last_name, middle_name=''):
	"""Return a full name, neatly formatted."""
	full_name = f"{first_name} {middle_name} {last_name}"
	return full_name.title()
	
print(get_formatted_name('jimi', 'hendrix'))
# Jimi Hendrix

print(get_formatted_name('john', 'hooker', 'lee'))
# John Lee Hooker
```
#### *Returning a dictionary*
```python
def build_person(first_name, last_name, age=None): 
	"""Return a dictionary of information about a person.""" 
	person = {'first': first_name, 'last': last_name} 
	if age:
		person['age'] = age
	return person
print(build_person('jimi', 'hendrix', age=27))
# {'first': 'jimi', 'last': 'hendrix', 'age': 27}
```
You can think of `None` as a placeholder value. In conditional tests, `None` evaluates to `False`.
## Passing a list
```python
def greet_users(names):
	"""Print a simple greeting to each user in the list.""" 	
	for name in names:
		msg = f"Hello, {name.title()}!"
		print(msg)

usernames = ['hannah', 'ty', 'margot'] 
greet_users(usernames)
```
* Programs with functions are easier to extend and maintain than the version without functions
* Every function should have one job
* You can call a function from another function
#### *Preventing a function from modifying a list*
You can pass the function a copy of the list, not the original one. Any changes the function makes to the list will affect only the copy, leaving the original list intact.
```python
function_name(list_name[:])
```
>You should have a specific reason to pass a copy. It’s more efficient for a function to work with an existing list to avoid using the time and memory needed to make a separate copy, especially when you’re working with large lists.

## Passing an arbitrary number of arguments
```python
def make_pizza(*toppings):
	"""Print the list of toppings that have been requested."""
	print(toppings)

make_pizza('pepperoni')
# ('pepperoni',)
make_pizza('mushrooms', 'green peppers', 'extra cheese')
# ('mushrooms', 'green peppers', 'extra cheese')
```
The asterisk in the parameter name `*toppings` tell Python to make an empty tuple called `toppings` and pack whatever values it receives into this tuple.
#### *Mixing positional and arbitrary arguments*
If you want a function to accept several different kinds of arguments, the parameter that accepts an arbitrary number of arguments must be placed last in the function definition.
```python
def make_pizza(size, *toppings):
	"""Summarize the pizza we are about to make.""" 
	print(f"\nMaking a {size}-inch pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")

make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
>You’ll often see the generic parameter name `*args`, which collects arbitrary positional arguments like this.
#### *Using arbitrary keyword arguments*
```python
def build_profile(first, last, **user_info): 
	"""Build a dictionary containing everything we know about a user."""
	user_info['first_name'] = first
	user_info['last_name'] = last
	return user_info
	
user_profile = build_profile('albert', 'einstein', 		
							location='princeton', 	
							field='physics')
print(user_profile)
# {'location': 'princeton', 'field': 'physics', 'first_name': 'albert', 'last_name': 'einstein'}
```
The double asterisks before the parameter `**user_info` cause Python to create an empty dictionary called `user_info` and pack whatever name-value pairs it receives into this dictionary.
>You’ll often see the parameter name `**kwargs` used to collect non-specific keyword arguments.

## Storing your functions in modules
Storing your functions in a separate file allows you to hide the details of your program’s code and focus on its higher-level logic. It also allows you to reuse functions in many different programs. When you store your functions in separate files, you can share those files with other programmers without having to share your entire program. Knowing how to import functions also allows you to use libraries of functions that other programmers have written.
#### *Importing an entire module*
A *module* is a file ending in *.py* that contains the code you want to import into your program.
```python
def make_pizza(size, *toppings):
	"""Summarize the pizza we are about to make.""" 
	print(f"\nMaking a {size}-inch pizza with the following toppings:")
	for topping in toppings:
		print(f"- {topping}")
```
We save this file as *pizza.py*. We now make a separate file called *making_pizzas.py* in the same directory as *pizza.py*.
```python
import pizza

pizza.make_pizza(16, 'pepperoni')
pizza.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
#### *Importing specific functions*
```python
from module_name import function_0, functino_1, function_2

function_0()
function_1()
function_2()
```
With this synatx, you don't need to use the dot notation when you call a function.
#### *Using `as` to give a function an alias*
You can use a short, unique *alias*-an alternate name similar to a nickname for the function.
```python
from pizza import make_pizza as mp

mp(16, 'pepperoni')
mp(12, 'mushrooms', 'green peppers', 'extra cheese')
```
#### *Using `as` to give a module an alias*
You can also provide an alias for a module name.
```python
import pizza as p

p.make_pizza(16, 'pepperoni')
p.make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
The function names, which clearly tell you what each function does, are more important to the readability of your code than using the full module name.
#### *Importing all functions in a module*
```python
form pizza import *

make_pizza(16, 'pepperoni')
male_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```
>It's better to not use this approach when you're working with larger modules the you didn't write: if the module has a function name that matches an existing name in your project, you can get some unexpected results. Python may see several functions or variables with the same name, and instead of importing all the functions separately, it will overwrite the functions.


>The best approach is to import the function or functions you want, or import the entire module and use the dot notation.

## Styling functions
* Functions should have descriptive names, and these names should use lowercase letters and underscores. Module names should use these conventions too.
* Every function should have a comment that explains concisely what the function does. This comment should appear immediately after ther function defenition and use the docstring format.
* If you specify a default value for a parameter, no spaces should be used on either side of the equal sign. The same convention should be used for keyword arguments in function calls
* If a set of parameters causes a function's definition to be longer than 79 characters, press `enter` after the opening parenthesis on the definition line. On the next line, press `tab` twice to separate the list of arguments from the body of the function, which will only be indented one level.
```python
def function_name( 
		parameter_0, parameter_1,
		parameter_2, parameter_3,
		parameter_4, parameter_5):
	function body...
```
* If your program or module has more than one function, you can separate each by two blank lines to make it easier to see where one function ends and the next one begins.
* All `import` statements should be written at the beginning of a file. The only exception is if you use comments at the beginning of your file to describe the overall program.
#### *Next*
[[08 - Classes]]