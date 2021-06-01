## Reading from a file
Text files can contain weather data, traffic data, socioeconomic data, literary works, and more. Reading from a file is particularly useful in data analysis applications.
When you want to work with the information in a text file, the first step is to read the file into memory. You can read the entire contents of a file, or you can work through the file one line at a time.
#### *Reading an entire file*
```python
with open('pi_digits.txt') as file_object:
	contents = file_object.read()
print(contents)
```
The `open()` function needs the name of the file. Python looks for this file in the directory where the program that’s currently being executed is stored. The `open()` function returns an object representing the file. 
The keyword `with` closes the file once access to it is no longer needed (i.e. the `with` block finishes execution).
The `read()` method reads the entire contents of the file and returns it as one long string. It returns an empty string when it reaches the end of the file;this empty string shows up as a blank line. You can use `contents.rstrip()` to remove the extra blank line.
#### *File paths*
* **Relative file path**
A relative file path tells Python to look for a given location relative to the directory where the currently running program file is stored.
```python
with open('text_files/filename.txt') as file_object:
```
>Windows systems use a backslash (`\`) instead of a forward slash (`/`) when displaying file paths, but you can still use forward slashes in your code.

* **Absolute file path**
An absolute file path tells Python exactly where the file is on your computer regardless of where the progarm that's being executed is stored.
```python
file_path = '/home/ehmatthes/other_files/text_files/filename.txt'
with open(file_path) as file_object:
```
>If you try to use backslashes in a file path, you’ll get an error because the backslash is used to escape characters in strings. For example, in the path "`C:\path\to\file.txt`", the sequence `\t` is interpreted as a tab. If you need to use backslashes, you can escape each one in the path, like this: "`C:\\path\\to\\file.txt`".

#### *Reading line by line*
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
	for line in file_object:
		print(line)
```
```
3.1415926535 

8979323846 

2643383279

```
These blank lines appear because an invisible newline charcter is at the end of each line in the text file. The `print` function adds its own newline each time we call it.
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
	for line in file_object:
		print(line.rstrip())
```
```
3.1415926535 
8979323846 
2643383279
```
#### *Making a list of lines from a file*
```python
filename = 'pi_digits.txt'

with open(filename) as file_object:
	lines = file_object.readlines()
	
for line in lines:
	print(line.rstrip())
```
The `readlines()` method takes each line from the file and stores it in a list (i.e. it returns a list containing the lines).
#### *Working with a file's content*
```python
filename = 'pi_digits.txt'

pi_string = ''
with open(filename) as file_object:
	for line in file_object:
		pi_string += line.strip()
		
print(pi_string)
print(len(pi_string))
```
>When Python reads from a text file, it interprets all text in the file as a string. If you want to work with the value in a numerical context, you'll have to convert it to an interger using the `int()` function or convert it to a float using the `float()` function.

>You can replace any word in a string with a different word by using `replace('old', 'new')`.

## Writing to a file
#### *Writing an empty file*
To write text to a file, you need to call open() with a second argument telling Python that you want to write to the file.
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
	file_object.write('I love programming!')
```
You can open a file in *read mode* `'r'`, *write mode* `'w'`, *append mode* `'a'`, or a mode that allows you to read and write to the file `'r+'`. If you omit the mode argument, Python opens the file in read-only mode by default.
The `open()` function automatically creates the file you're writing to if it doesn't exist. However, be careful opening a file in write mode `'w'` because if the file does exist, Python will erase the contents of the file before returning the file object.
>Python can only write strings to a text file. If you want to store numerical data in a text file, you'll have to convert the data to string format first using the `str()` function.

#### *Writing multiple lines*
The `write()` function does not add any newlines to the text you write. So if you write more than one line without including newline characters `\n`, your file may not look the way you want it to.
```python
filename = 'programming.txt'

with open(filename, 'w') as file_object:
	file_object.write('I love programming!\n')
	file_object.write('I love creating new games!\n')

# I love programming. 
# I love creating new games.
```
>You can also use spaces, tab characters, and blank lines to format your output, just as you’ve been doing with terminal-based output.
#### *Appending to a file*
When you open a file in append mode, Python doesn’t erase the contents of the file before returning the file object. Any lines you write to the file will be added at the end of the file. If the file doesn’t exist yet, Python will create an empty file for you.
```python
filename = 'programming.txt'

with open(filename, 'a') as file_object:
	file_object.write('I also love finding meaning in large datasets.\n')
	file_object.write('I love creating apps that can run in a browser.\n')

# I love programming. 
# I love creating new games.
# I also love finding meaning in large datasets. 
# I love creating apps that can run in a browser.
```
## Exceptions
**Exceptions**: Special objects Python creates to manage errors that arise while a program is running.
If you write code that handels the exception, the program will continue running. If you don't handle the exception, the program will halt and show a traceback, which includes a report of the exception that was raised.
#### *Handling the `ZeroDivisionError` exception*
```python
print(5/0)
```
```
Traceback (most recent call last):
	File "division_calculator.py", line 1, in <module> 
		print(5/0)
ZeroDivisionError: division by zero
```
The last line of the traceback reports a `ZeroDivisionError`.
#### *Using `try`-`except` blocks*
```python
try:
	print(5/0)
except ZeroDivisionError:
	print('You can''t divide by zero!')
```
#### *Using exceptions to prevent crashes*
It’s bad that the program crashed, but it’s also not a good idea to let users see tracebacks. Nontechnical users will be confused by them, and in a malicious setting, attackers will learn more than you want them to know from a traceback. For example, they’ll know the name of your program file, and they’ll see a part of your code that isn’t working properly. A skilled attacker can sometimes use this information to determine which kind of attacks to use against your code.
#### *The `else` block*
Any code that depends on `try` block executing successfully goes in the `else` block.
```python
try:
	result = 5/0
except ZeroDivisionError:
	print('Can''t divide be zero!')
else:
	print(result)
```
The `try`-`except`-`else` block works like this: Python attempts to run the code in the `try` block. The only code that should go in a `try` block is code that might cause an exception to be raised. Sometimes you’ll have additional code that should run only if the `try` block was successful; this code goes in the `else` block. The `except` block tells Python what to do in case a certain exception arises when it tries to run the code in the `try` block.
#### *Handling the `FileNotFoundError` exception*
The file you’re looking for might be in a different location, the filename may be misspelled, or the file may not exist at all.
```python
filename = `alice.txt`

with open(filename, encoding='utf-8') as f:
	contents = f.read()
```
The `encoding` argument is needed when your system's default encoding doesn't match the encoding of the file that's being read.
```
Traceback (most recent call last):
	File "alice.py", line 3, in <module>
		with open(filename, encoding='utf-8') as f:
FileNotFoundError: [Errno 2] No such file or directory: 'alice.txt'
```
The `open()` function produces the error, so to handle it, the `try` block will begin with the line that contains `open()`.
```python
filename = 'alice.txt'

try:
	with open(filename, encoding='utf-8') as f:
		contents = f.read()
except FileNotFoundError:
	print(f"Sorry, the file {filename} doesn't exist.")
```
#### *Analyzing text*
```python
filename = 'alice.txt'

try:
	with open(filename, encoding='utf-8') as f:
		contents = f.read()
except FileNotFoundError:
	print(f"Sorry, the file {filename} doesn't exist.")
else:
	words = contents.split()
	num_words = len(words)
	print(f"The file {filename} contains {num_words} words.")
```
The `split()` method separates a string into parts wherever it finds a space and stores all the parts of the string in a list.
>Project Gutenberg (`http://gutenberg .org/`) maintains a collection of literary works that are available in the public domain, and it’s a great resource if you’re interested in working with literary texts in your programming projects.

#### *Working with multiple files*
```python
def count_words(filename):
	"""Count the approximate number of words in a file.""" 
	try:
		with open(filename, encoding='utf-8') as f: 
			contents = f.read()
	except FileNotFoundError:
		print(f"Sorry, the file {filename} does not exist.")
	else:	
		words = contents.split() num_words = len(words)
		print(f"The file {filename} has about {num_words} words.")
		
filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
	count_words(filename)
```
#### *Failing silently*
Python has a `pass` statement that tells it to do nothing in a block.
```python
def count_words(filename):
	"""Count the approximat number of words in a file."""
	try:
		--snip--
	except FileNotFoundError:
		pass
	else:
		--snip--
```
No traceback is produced, and there’s no output in response to the error that was raised.
The `pass` statement also acts as a placeholder. It’s a reminder that you’re choosing to do nothing at a specific point in your program’s execution and that you might want to do something there later. For example, in this program we might decide to write any missing filenames to a file called `missing_files.txt`. Our users wouldn’t see this file, but we’d be able to read the file and deal with any missing texts.
#### *Deciding which error to report*
Python’s error-handling structures give you finegrained control over how much to share with users when things go wrong; it’s up to you to decide how much information to share.
Well-written, properly tested code is not very prone to internal errors, such as syntax or logical errors. But every time your program depends on something external, such as user input, the existence of a file, or the availability of a network connection, there is a possibility of an exception being raised.
>`ValueError` is an exception that's raised when you want to convert a text that's not a number to an `int`.

>You can use `count('word')` method to find out how many times a word or phrase appears in a string (`string.count('word')`.

## Storing data
When a programis closed, you’ll almost always want to save the information they entered. A simple way to do this involves storing your data using the `json` module.
The `json` module allows you to  dump simple Python data structures into a file and load the data from that file the next time the program runs. You can also use `json` to shar data between different Python programs.
>The JSON data format is not specific to Python, so you can share data you store in the JSON fomat with people who work in many other programming languages.

>The JSON (JavaScript Object Notation) format was originally developed for JavaScript. However, it has since become a common format used by many languages.

#### *Using `json.dump()` and `json.load()`*
The `json.dump()` function takes two arguments: a piece of data to store and a file object it can use to store the data.
```python
import json

numbers = [3, 9, 93, 20, 87]

filename = 'numbers.json'
with open(filename, 'w') as f:
	json.dump(numbers, f)
```
`json.load()` reads the list back into memory.
```python
import json

filname = 'numbers.json'
with open(filename, 'w') as f:
	numbers = json.load(f)
```
#### *Saving and reading user-generated data*
The following program stores the user's name:
```python
import json

username = input('What is your name? ')

filename = 'username.json'
with open(filename, 'w') as f:
	json.dump(username, f)
	print(f"We will remember you when you come back, {username}!")
```
The following program greets a user whose name has already been stored:
```python
filename = 'username.json'
with open(filename) as f:
	username = json.load(f)
	print(f"Welcome back, {username}")
```
Combining the two programs, we get:
```python
import json

filename = 'username.json'
try:
	with open(filename) as f:
		username = json.load(f)
except FileNotFoundError:
	username = input('What is your name? ')
	with open(filename, 'w') as f:
		json.dump(username, f)
		print(f"We will remember you when you come back, {username}!")
else:
	print(f"Welcome back, {username}")
```
#### *Refactoring*
*Refactoring* is breaking up the code into series of functinos that have specific jobs.
```python
import json

def get_stored_username():
	"""Get storred username if available."""
	filename = 'username.json'
	try:
		with open(filename) as f:
			username = json.load(f)
	except FileNotFoundError:
		return None
	else:
		return username

def get_new_username():
	"""Prompt for a new username."""
	filename = 'username.json'
	username = input('What is your name? ')	
	with open(filename, 'w') as f:
		json.dump(username, f)
	return username
	
def greet_user():
	"""Greet the user by name."""
	username = get_stored_username
	if username:
		print(f"Welcome back, {username}")
	else:
		username = get_new_username()
		print(f"We'll remember you when you come back, {username}!")
	
greet_user()
```
#### *Next*
[[10 - Testing your code]]