## Testing a function
```python
def get_formatted_name(first, last):
	"""Generate a neatly formatted full name."""
	return f"{first} {last}".title()
	
first = input("Give me a first name: ")
last = input("Give me a last name: ")
formatted_name = get_formatted_name(first, last)
print(f"Neatly formatted name: {formatted_name}")
```
It can become tedious to test our code by entering names every time we modify `get_formatted_name()`. Fortunately, Python provides an efficient way to automate the testing of a function's output.
#### *Unit tests and test cases*
The module `unittest` form the Python standard library provides tools for testing code. A ==*unit test*== verifies that one aspect of a function's behavior is correct. A ==*test case*== is a ==collection of unit tests== that together prove that a function behaves as it's supposed to, within the full range of situations you expect it to handle.
A good test case <mark style="background-color: green">considers</mark> all the possible kinds of input a function could receive and includes tests to represent each of these situations.

#### *A passing test*
To write a test case for a function:
1. import the `unittest` module and the function you want to test. 
2. Then create a class that inherits from `unittest.TestCase`, and write a series of methods to test different aspects of your function’s behavior.
```python
import unittest
from name_function import get_formatted_name

class NamesTestCases(unitest.TestCase):
	"""Test for 'name_function.py'."""
	
	def test_first_last_name(self):
		"""Do names like 'Janis Jolpin' work?"""
		formatted_name = get_formatted_name('janis', 'joplin')
		sefl.assertEqual(formatted_name, 'Janis Joplin')
		
if __name__ == '__main__':
	unittest.main()
```
`NamesTestCase` contains a single method that tests one aspect of `get_formatted_name()`.
Any method that starts with `test_` will be run automatically when we run `text_name_function.py`. Within this test method, we call the function we want to test.
Assert methods verify that a result you receive matches the result you expected to receive.
We’re going to run this file directly, but it’s important to note that many testing frameworks import your test files before running them. When a file is imported, the interpreter executes the file as it’s being imported.
If this file is being run as the main program, the value of `__name__` is set to `__main__`. In this case, we call `unittest.main()`, which runs the test case. When a testing framework imports this file, the value of `__name__` won’t be `__main__` and this block will not be executed.
```
.
---------------------------------------------------------------------
Ran 1 test in 0.001s

OK
```
The dot tells us that a single test passed.
The next line tells us that Python ran one test, and it took less than 0.001 seconds to run. The final `OK` tells us that all unit tests in the test case passed.
#### *A failing test*
```python
def get_formatted_name(first, middle, last):
	"""Generate a neatly formatted full name."""
	return f"{first} {middle} {last}"
```
This version should work for people with middle names, but when we test it, we see that we've broken the function for people without middle name.
```
E
======================================================================
ERROR: test_first_last_name (__main__.NamesTestCase)
----------------------------------------------------------------------
Traceback (most recent call last):
	File "test_name_function.py", line 8, in test_first_last_name 
		formatted_name = get_formatted_name('janis', 'joplin')
TypeError: get_formatted_name() missing 1 required positional argument: 'last'

----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (errors=1)
```
`E` tells us one unit test in the test case resulted in an error.
Next we see that `test_first_lase_name()` in `NamesTestCase` caused the error.
Finally, we see an additional message that the overall test case failed and that one error occurred when running the test case.
#### *Responding to a failed test*
The best option to respond to that error is to make the middle name optional.
```python
def get_formatted_name(first, last, middle=''):
	"""Generate a neatly formatted full name."""
	if middle:
		full_name = f"{first} {middle} {last}"
	else:
		full_name = f"{first} {last}"
	return full_name.title()
```
```
.
---------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```
Fixing our function was easy because the failed test helped us identify the new code that broke existing behavior.
#### *Adding new tests*
```python
import unittest
from name_function import get_formatted_name

class NamesTestCases(unitest.TestCase):
	"""Test for 'name_function.py'."""
	
	def test_first_last_name(self):
		"""Do names like 'Janis Jolpin' work?"""
		formatted_name = get_formatted_name('janis', 'joplin')
		sefl.assertEqual(formatted_name, 'Janis Joplin')
		
	def test_first_last_middle_name(self):
		"""Do names like 'Wolfgang amadeus Mozart' work?"""
		formatted_name = get_formatted_name('wolfgang', 'mozart', 'amadeus')
		self.assertEqual(formatted_name, 'Wolfgang amadeus Mozart')
		
if __name__ == '__main__':
	unittest.main()
```
```
..
----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK
```
## Testing a class
#### *A variety of assert methods*
Python provides a number of assert methods in the `unittest.TestCase` class. You can use them only in a class that inherits from `unittest.TestCase`.

| Method | Use |
| --- | --- |
| `assertEqual(a, b)` | Verify that `a == b` |
| `assertNotEqual(a, b)` | Verify that `a != b` |
| `assertTrue(x)` | Verify that `x` is `True` |
| `assertFalse(x)` | Verify that `x` is `False` |
| `assertIn(item, list)` | Verify that `item` is in `list` |
| `assertNotIn(item, list)` | Verify that `item` in not in `list` |
#### *A class to test*
Testing a class is similar to testing a function—much of your work involves ==testing the behavior of the methods in the class==.
In the file `survey.py`:
```pyhton
class AnonymousSurvey:
	"""Collect anonymous answers to a survey question."""
	
	def __init__(self, question):
		"""Store a question, and prepare to store responses."""
		self.question = question
		self.responses = []
		
	def show_question(self):
		"""Show the survey question."""
		print(self.question)
		
	def store_response(self, new_response):
		"""Store a single response to the survey."""
		self.responses.append(new_response)
		
	def show_results(self):
		"""Show all the responses that have been given."""
		print("Survey results:")
		for response in self.responses:
			print(f"- {response}")
```
Now we writes a program that uses the class:
```python
from survey import AnonymousSurvey

# Define a question, and make a survey.
question = "What language did you first learn to speak?"
my_survey = AnonymousSurvey(question)

# Show the question, and store responses.
my_survey.show_question()
print("Enter 'q' at any time to quit.\n")
while True:
	response = input("Language: ")
	if response == 'q':
		break
	my_survey.store_response(response)
	
# Show the survey results
print("\nThank you for participating!")
my_survey.show_results()
```
If we try implementing changes to the class, we risk of affecting the current behavior.
Let's write a test that verifies one aspect of the way `AnonymousSurvey` behaves.
```python
import unittest
from survey import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
	"""Tests for the class AnonymousSurvey."""
	
	def test_store_single_response(self):
		"""Test that a single response is stored properly."""
		question = "What language did you first learn to speak?"
		my_survey = AnonymousSurvey(question)
		my_survey.store_response('English')
		self.assertIn('English', my_survey.responses)
		
	def test_store_three_responses(self):
		"""Test that three individual responses are stored properly."""
		question = "What language did you first learn to speak?"
		my_survey = AnonymousSurvey(question)
		responses = ['English', 'Spanish', 'Mandarin']
		for response in responses:
			my_survey.store_response(response)
		for response in responses:
			assertIn(response, my_survey.responses)
		
if __name__ == '__main__':
	unittest.main()
```
To test the behavior of a class, we need to make an instance of the class.
The first method in the test case will verify that when we store a response to the survey question, the response ends up in the survey's list of responses.
The second method asserts that three responses are in the survey's list of responses.
>We notice that theses tests are a bit repetitive, so we'll use another feature of `unittest` to make them more efficient.

#### *The `setUp()` method*
The `unittest.TestCase` class has a `setUp()` method that allows you to create an instance of `AnonymousSurvey` and responses just **once** and then use them in each of your test methods. When you include a `setUp()` method in a `TestCase` class, Python runs the `setUp()` method before running each method starting with `test_`. Any objects created in the `setUp()` method are then available in each test method you write.
```python
import unittest
from survey import AnonymousSurvey

class TestAnonymousSurvey(unittest.TestCase):
	"""Tests for the class AnonymousSurvey."""
	
	def setUp(self):
		"""Create a survey and a set of responses for use in all test methods."""
		question = "What language did you first learn to speak?"
		self.my_survey = AnonymousSurvey(question)
		self.responses = ['English', 'Spanish', 'Mandarin']
		
	def test_store_single_response(self):
		"""Test that a single response is stored properly."""
		self.my_survey.store_response(self.responses[0])
		self.assertIn(self.responses[0], self.my_survey.responses)
		
	def test_store_three_responses(self):
		"""Test that three individual responses are stored properly."""
		for response in self.responses:
			self.my_survey.store_response(response)
		for response in self.responses:
			assertIn(response, self.my_survey.responses)

if __name__ = '__main__':
	unittest.main()
```
The objects created in `setUp()` are prefixed by `self`, so they can be used anywhere in the class.
The tests would be particularly useful when trying to expand `AnonymousSurvey` to handle multiple responses for each person.

>When a test case is running, Python prints one character for each unit test as it is completed. A passing test prints a dot, a test that results in an error prints an E, and a test that results in a failed assertion prints an F. This is why you’ll see a different number of dots and characters on the first line of output when you run your test cases. If a test case takes a long time to run because it contains many unit tests, you can watch these results to get a sense of how many tests are passing.