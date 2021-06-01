## How `input()` works?
The `input()` function pauses your program and waites for the user to enter some text.
The `input()` function takes one argument: the **prompt**, or instructions, that we want to display to the user so they know what to do.
#### *Writing clear prompts*
```python
prompt = "If you tell us who you are, we can personalize the messages you see."
prompt += "\nWhat is your first name? "

name = input(prompt)
print(f"Hello {name}!")
```
* Add a space at the end of your prompt
* Assign the prompt to a variable if it's too long and pass that variable to the `input()` function
#### *Using `int()` to accept numerical input*
When you use the input() function, Python interprets everything the user enters as a string.
The `int()` function tells Python to treat the input as a numerical value.
```python
age = input("How old are you?")
age = int(age)
print(age >= 18)
```
#### *The modulo operator*
```python
print(5 % 3)
# 2
```
## `while` loops
```python
prompt = "Enter 'quit' to end the program: "
message = ""
while message != "quit":
	message = input(prompt)
	if message != "quit":
		print(message)
```
#### *Using a flag*
In complicated programs where many different events could cause the program to stop running, you can define one variable that determines whether or not the entire program is active. This variable is called a **flage** and it acts as a signal to the program.
```python
prompt = "Enter 'quit' to end the program: "

active = true
while active:
	message = input(prompt)
	
	if message == 'quit':
		active = false
	else:
		print(message)
```
#### *Using `break` to exit a loop*
```python
prompt = "\nEnter the name of a city you have visited:"
prompt += "\n(Enter 'quit' when you are finished.) "

while True:
	city = input(prompt)
	
	if city == 'quit':
		break
	else:
		print(f"I'd love to go to {city.title()}")
```
>You can use `break` statement in any of Python's loops.

#### *Using `continue` in a loop*
Rather than breaking out of a loop entirely without the rest of its code, you can use the `continue` statement to return to the beginning of the loop based on the result of a conditional test.
```python
# Printing the odd numbers from 1 to 10
current_number = 0
while current_number < 10:
	current_number += 1
	if current_number % 2 == 0:
		continue
	print(current_number)
```
#### *Avoiding infinite loops*
Every programmer accidentally writes an infinite `while` loop form time to time. If your program gets stuck in an infinite loop, press `CTRL`+`C`.
## Using a `while` loop with lists and dictionaries
To modify a list as you work through it, use a `while` loop instead of a `for` loop.
#### *Moving items from one list to another*
```python
unconfirmed_users = ['alice', 'brian', 'candace']
confirmed_users = []

while unconfirmed_users:
	current_user = unconfirmed_users.pop()
	print(f"Verifying user: {current_user.title()}")
	confirmed_users.append(current_user)
```
#### *Removing all instances of specific values from a list*
```python
pets = ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']
print(pets)
# ['dog', 'cat', 'dog', 'goldfish', 'cat', 'rabbit', 'cat']

while 'cat' in pets:
	pets.remove('cat')
	
print(pets)
# ['dog', 'dog', 'goldfish', 'rabbit']
```
#### *Filling a dictionary with user input*
```python
responses = {}

polling_active = True

while polling_active:
	name = input("\nWhat is your name? ")
	response = input("Which mountain would you like to climb someday? ")
	
	responses[name] = response
	repeat = input("Would you like to let another person respond? (yes/ no) ") 
	if repeat == 'no':
		polling_active = False
print("\n--- Poll Results ---")
for name, response in responses.items():
	print(f"{name} would like to climb {response}.")
```
#### *Next*
[[07 - Functions]]