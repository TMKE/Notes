## What happens when you run a file.py

- The editor runs the file through the *Python interpreter*, which reads through the program and determines what each word in the program means.

  > An **interpreter** is a computer program that directly executes instructions written in a programming or scripting language, without requiring them previously to have been compiled into a machine language program.

- The editor highlights different parts of the program in different ways (syntax highlighting).
## Variables
Every variable is connected to a *value*, which is the information associated with that variable.

### *Naming and using variables (rules)*

- Variable names can contain only letters, numbers, and underscores.
- They can start with a letter or an underscore, but not with a number.
- Spaces are not allowed in variable names, use underscores instead.
- Python reserved keywords and built-in functions (like `print`) cannot be used as variable names
- Variable names should be short but descriptive (`name` is better than `n`)
- Pay attention when using lowercase *l* and uppercase *O*, because they could be confused with the *1* and *0*.

### *Variables as labels*

- It's better to think of variables as *labels* assigned to values.
- You can also say that a variable references a certain value.
## Strings
- A *string* is a _series of characters_. Anything inside quotes is considered a string in Python, and you can use a single or double quotes around your strings.
- This flexibility allows you to use quotes and apostrophes within your string

### *Changing case in a string with methods*

```python
name = "ada lovelace"
print(name.title())

'''The title() method changes each word to title case.
It's useful for names'''

print(name.upper())

'''upper() changes a string to all uppercase'''

print(name.lower())

'''lower() changes a string to all lowercase
It's useful for storing data'''
```

### *Using variables in strings*
```python
first_name = "ada"
last_name = "lovelace"
full_name= f"{first_name} {last_name}"
print(f"Hi, {full_name.title()}")
```
These strings are called _f-strings_. The _f_ is for _format_, because Python formats the string by replacing the name of any variable in braces with its value.

>In Python 3.5 or earlier, use `format()` rather than _f_ syntax:
>
>```python
>full_name = "{} {}".format(first_name, last_name)
>```
>
>PS. It works with the newer versions.
### _Adding whitespace to strings with tabs or newlines_
```python
print("Languages:\n\tPython\n\tC\n\tJavaScript")
```
- `\n` is used to add a newline in a string.
- `\t` is used to add tab to text.
### _Stripping whitespace_
To ensure that no whitespace exists at the right end of a string, use `rstrip()` method

```python
favorite_language = 'python '
# 'python ' 
favorite_language = favorite_language.rstrip()
# 'python'
```
You can also strip whitespace from the left side of a string using `lstrip()` method, or from both sides at once using `strip()`

```python
favorite_language = ' python '
# ' python ' 
print(favorite_language.rstrip())
# ' python'
print(favorite_language.lstrip())
# 'python '
print(favorite_language.strip())
# 'python'
```
### _Avoiding syntax errors with strings_
>A syntax error occurs when _Python_ doesn't recognize a section of your program as valid _Python_ code
```python
print("One of Python's strengths is its diverse community.")
# This line works fine, no error here
print('One of Python's strengths is its diverse community.')
# This line causes a syntax error,
# the apostrophe is considered as the end of the string,
# and the rest is considered as Python code
```
## Numbers
### _Integers_
- You can add `+`, subtract `-`, multiply `*`, and divide `/` integers
- Python uses `**` to represent exponents
- Python supports the order of operations
### _Floats_
Any number with a decimal point is a _float_

```python
print(0.2 + 0.1)
# the result is: 0.30000000000000004
```
_This happens in all languages given how computers have to represent numbers internally_
### _Integers and floats_
- Dividing two numbers always gives a float, even if they are integers
- Mixing an integer and a float in any other operation gives a float as well
### _Underscores in numbers_
```python
one_million = 1_000_000
# Python ignores the underscores when storing these kinds of values
```
>This feature is only available in _Python 3.6_ and later
### _Multiple assignment_
```python
x, y, z = 0, 0, 0
```
- You can assign values to more than one variable using a single line
- This technique is used most often when initializing a set of numbers
### _Constants_
- Python doesn't have built-in constant types
- Python programmers use all capital letters to indicate a variable should be treated as a constant and never be changed
```python
MAX_CONNECTIONS = 500
```
## Comments
- The hash mark `#` indicates this line is a comment
- You should write meaningful comments explaining what your code is supposed to do
## The Zen of Python
- Avoid complexity and aim for simplicity whenever possible
- You can access the set of principles for writing good Python code by entering `import this` into your interpreter