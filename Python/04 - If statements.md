## Conditional tests
At the heart of every `if` statement is an expression that can be evaluated as `True` or `False` and is called a __*conditional test*__ (using the *equality operator* `==`). If the test evaluates to `True`/`False`, Python executes/ignores the code following the `if` statement.
### *Ignoring case when checking for equality*
Testing for equality is case sensitive.
```python
print('Audi' == 'audi')
# False

print('Audi'.lower() == 'audi')
# True
```
### *Checking for inequality*
We use the inequality operator `!=`.
```python
requested_topping = 'mushrooms'
if requested_topping != 'anchovies':
	print("Hold the anchovies!")
# Hold the anchovies
```
### *Numerical comparisons*
```python
age = 18

print(age == 18)
# True

print(age >= 19)
# False
```
### *Checking multiple conditions*
#### _Using `and`:_

```python
age = 18
print(age < 19 and age > 17)
# True
```
>To improve readability, you can use parentheses around individual tests.
#### _Using `or`:_

```python
age = 18
print((age < 19) or (age > 17))
# True
```
### *Checking whether a value is in a list*
```python
requested_toppings = ['mushrooms', 'onions', 'pineapple']
print('mushrooms' in requested_toppings)
# True
print('pepperoni' in requested_toppings)
# False
```
### _Checking whether a value is not in a list_
```python
requested_toppings = ['mushrooms', 'onions', 'pineapple']
print('mushrooms' not in requested_toppings)
# False
print('pepperoni' not in requested_toppings)
# True
```
### _Boolean expressions_
A Boolean expression is just another name for a conditional test.
## `if` statements
### _Simple `if` statements_
```python
age = 19
if age >= 18:
	print("You are old enough to vote!") 
	print("Have you registered to vote yet?")
```
### _`if`-`else` statements_
```python
age =17
if age >= 18:
	print("You are old enough to vote!") 
	print("Have you registered to vote yet?")
else:
	print("Sorry, you are too young to vote.")
	print("Please register to vote as soon as you turn 18!")
```
### _The `if`-`elif`-`else` chain_
```python
age = 12
if age < 4: 
	price = 0
elif age < 18:
	price = 25
else:
	price = 40
print(f"Your admission cost is ${price}.")
# Your admission cost is $25
```
### _Using multiple `elif` blocks_
You can use as many `elif` blocks as you like.
### _Omitting the `else` block_
Python doesn't not require an `else` block at the end of an `if`-`elif` chain.
The `else` block is a *catchall* statement. It matches any condition that wasn't matched by a specific `if` or `elif` test, and that can sometimes include invalid or even malicious data.

### _Testing multiple conditions_
Sometimes it is important to check all of the conditions of interest. In this case, you should use a series of `if` statements with no `elif` or `else` blocks.
```python
requested_toppings = ['mushrooms', 'extra cheese']

if 'mushrooms' in requested_toppings:
	print("Adding mushrooms.")
if 'pepperoni' in requested_toppings:
	print("Adding pepperoni")
if 'extra cheese' in requested_toppings:
	print("Adding extra cheese")
```
## Using `if` statements with lists
### _Checking if a list is not empty_
```python
requested_toppings = [] 
if requested_toppings:
	for requested_topping in requested_toppings: 
		print(f"Adding {requested_topping}.") 
	print("\nFinished making your pizza!")
else:
	print("Are you sure you want a plain pizza?")

# Are you sure you want a plain pizza?
```
An empty list evaluates to `False`.
### _Using multiple lists_
```python
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']
requested_toppings = ['mushrooms', 'french fries', 'extra chees']

for requested_topping in requested_toppings:
	if requested_topping in available_toppings:
		print(f"Adding {requested_topping}.")
	else:
		print(f"Sorry, we don't have {requested_topping}.")
print("\nFinished making your pizza!")

# Adding mushrooms.
# Sorry, we don't have french fries.
# Adding extra cheese.
#
# Finished making your pizza!
```
>Note that the list of available toppings could be a tuple if the pizzeria has a stable selection of toppings.
## Styling `if` statement
The only recommendation PEP 8 provides for styling conditional tests is to use a single space around comparison operators, such as `==`, `>=`, `<=`.