Making an object from a class is called *instanciation*, and you work with *instances* of a class.
## Creating and using a class
#### *Creating a class*
```python
class Dog:
	"""A simple attempt to model a dog"""
	
	def __init__(self, name, age):
		"""initialize name and age attributes"""
		self.name = name
		self.age = age
		
	def sit(self):
		"""Simulate a dog sitting in response to a command"""
		print(f"{self.name} is now sitting.")
		
	def roll_over(self):
		"""Simulate rolling over in response to a command."""
		print(f"{self.name} rolled over")
```
Classes names are capitalized.
* **The `__init__()` method**
A function that's part of a class is a method. The `__init()__` method is a special method that Python runs automatically whenever we create a new instance based on the `Dog` class.
The underscores prevent Python form conflicting default methods names with your method names.
The `self` parameter is required in the method definition because when Python calls this method later, the method call will automatically pass the self argument, and it must come first before the other parameters.
Variables that are accessible through instances (like `self.name = name`) are called *attributes*.
#### *Making an instance from a class*
```python
class Dog:
	--snip--
	
dog_0 = Dog('Willie', 6)
```
When Python reads the line`dog_0 = Dog('Willie', 6)`, it calls the `__init()__` method with the arguments `'Willie'` and `6`.
* __Accessing attributes__
Use the dot notation.
```python
dog_0.name
```
* **Calling methods**
Use the dot notation to call methods.
```python
my_dog.sit()
my_dog.roll_over()
```
* **Creating multiple instances**
```python
dog_1 = Dog('Luby', 3)
dog_0.sit()
# Willie is now sitting.
dog_1.sit()
# Lucy in now sitting.
```
## Working with classes and instances
```python
class Car:
	"""A simple attempt to represent a car."""
	
	def __inti__(self, manufacturer, model, year):
		"""Initialize attributes to describe a car."""
		self.manufacturer = manufacturer
		self.year = year
		self.model = model
	
	def get_descriptive_name(self):
		"""Return a neatly formatted descriptive name."""
		return f"{self.year} {self.manufacturer} {self.model}"
		
car_0 = Car('Audi', 'a4', 2019)
print(car_0.get_descriptive_name())
# 2019 Audi a4
```
#### *Setting a default value for an attribute*
When an instance is created, attributes can be defined without being passed in as parameters. These attributes can be defined in the `__init__()` method, where they are assigned a default value.
```python
class Car:
	"""A simple attempt to represent a car."""
	
	def __inti__(self, manufacturer, model, year):
		"""Initialize attributes to describe a car."""
		self.manufacturer = manufacturer
		self.year = year
		self.model = model
		self.odometer_reading = 0
	
	def get_descriptive_name(self):
		"""Return a neatly formatted descriptive name."""
		return f"{self.year} {self.manufacturer} {self.model}"
	
	def read_odometer(self):
		"""Print a statement showing the car's mileage"""
		print(f"This car has {self.odometer_reading} miles on it")
		
car_0 = Car('Audi', 'a4', 2019)
print(car_0.get_descriptive_name())
# 2019 Audi a4
car_0.read_odometer()
# This car has 0 miles on it.
```
#### *Modifying attribute values*
* **Directly**
The simplest way to modify the value of an attribute is to access the attribute directly through an instance.
```python
class Car:
	--snip--
	
car_0 = Car('Audi', 'a4', 2019)
print(car_0.get_descriptive_name())
# 2019 Audi a4
car_0.odometer_reading = 23
car_0.read_odometer()
# This car has 23 miles on it.
```
* **Through a method**
```python
class Car:
	--snip--
	
	def update_odometer(self, mileage):
		"""Set the odometer reading to the given value"""
		self.odometer_reading = mileage
	
car_0 = Car('Audi', 'a4', 2019)
print(car_0.get_descriptive_name())
# 2019 Audi a4
car_0.update_odometer(23)
car_0.read_odometer()
# This car has 23 miles on it.
```
## Inheritance
If the class you’re writing is a specialized version of another class you wrote, you can use *inheritance*. When one class inherits from another, it takes on the attributes and methods of the first class. The original class is called the *parent class*, and the new class is the *child class*.
#### *The `__init__()` method for a child class*
```python
class Car:
	--snip--

class ElectricCar(Car):
	"""Represent aspects of a car, specific to electric vehicules."""
	
	def __init__(self, manufacturer, model, year):
		"""Initialize attributes of the parent class"""
		super().__init__(manufacturer, model, year)
		
my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
# 2019 Tesla Model S
```
The `super()` function is a special function that allows you to call a method from the parent class. The name super comes from a convention of calling the parent class a *superclass* and the child class a *subclass*.
#### _Definig attributes and methods for the child class_
You can add any new attributes and methods necessary to differentiate the child class from the parent class.
```python
class Car:
	--snip--

class ElectricCar(Car):
	"""Represent aspects of a car, specific to electric vehicules."""
	
	def __init__(self, manufacturer, model, year):
		"""
		Initialize attributes of the parent class.
		Then initialize attributes specific to an electric car
		"""
		super().__init__(manufacturer, model, year)
		self.battery_size = 75
		
	def describe_battery(self):
		"""Print a statement describing the battery size."""
		print(f"This car has a {self.battery_size}-kWh battery")
		
my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
# 2019 Tesla Model S
my_tesla.describe_battery()
# This car has a 75-kWh battery.
```
#### *Overriding methods from the parent class*
To do this, you define a method in the child class with the same name as the method you want to override in the parent class. Python will disregard the parent class method and only pay attention to the method you define in the child class.
```python
class ElectricCar(Car):
	--snip--
	
	def fill_gas_tank(self):
		"""Electric cars don't have gas tanks."""
		print("This car doesn't need a gas tank!")
```
If someone tries to call `fill_gas_tank()` with an electric car, Python will ignore the method `fill_gas_tank()` in `Car` and run this code instead.
#### *Instances as attributes*
You can break your large class into smaller classes that work together if you recognize that part of it can be written as separate classes.
```python
class Car:
	--snip--
	
class Battery:
	"""A simple attempt to model a battery for an electric car."""
	
	def __init__(self, battery_size=75):
		"""Initialize the battery's attributes.""" 
		self.battery_size = battery_size
		
	def describe_battery(self):
		"""Print a statement describing the battery size."""
		print(f"This car has a {self.battery_size}-kWh battery.")
		
class ElectricCar(Car):
	""Represent aspects of a car, specific to electric vehicles."""
	
	def __init__(self, manufacturer, model, year):
		"""
		Initialize attributes of the parent class.
		Then initialize attributes specific to an electric car
		"""
		super().__init__(manufacturer, model, year)
		self.battery = Battery()
	
my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
# 2019 Tesla Model S
my_tesla.battery.describe_battery()
# This car has a 75-kWh battery.
```
Now we can describe the battery in as much detail as we want without cluttering the `ElectricCar` class.
```python
class Car:
	--snip--
	
class Battery:
	--snip--
	
	def get_range(self):
		"""Print a statement about the range this battery provides."""
		if self.battery_size == 75:
			range = 260
		elif self.battery_size == 100:
			range = 315
		print(f"This car can go about {range} miles on a full charge.")
		
class ElectricCar(Car):
	--snip--
	
my_tesla = ElectricCar('tesla', 'model s', 2019)
print(my_tesla.get_descriptive_name())
# 2019 Tesla Model S
my_tesla.battery.describe_battery()
# This car has a 75-kWh battery.
my_tesla.battery.get_range()
# This car can go about 260 miles on a full charge.
```
## Importing classes
#### *Importing a single class*
In the file *car.py*:
```python
"""A claas than ca be used to represent a car."""

class Car:
	--snip--
```
We include a module-level docstring that briefly describes the contents of this module.
In a separate file:
```pyhton
from car import Car

car_0 = Car('audi', 'a4', 2019)
```
#### *Storing multiple classes in a module*
Each class in a module should be related somehow.
```python
class Car:
	--snip--
	
class Battery:
	--snip--
	
class ElectricCar(Car):
	--snip--
```
```python
from car import Car, Battery, ElectricCar

my_tesla = ElectricCar('tesla', 'model s', 2019)
```
#### *Importing an entire module*
```python
import car
```
You can use dot notation to access the classes you need.
#### *Importing all classes form a module*
```python
from car import *
```
This is not recommended.
#### *Importing a module into a module*
In the file *electric_car.py*:
```python
"""A set of classes that can be used to represent electric cars."""

from car import Car

class Battery:
	--snip--
	
class ElectricCar(Car):
	--snip--
```
With this approach, you don't need to store related functions in a single file. You can import from each module separately.
```python
from car import Car
from electric_car import ElectricCar
```
#### *Using alias*
```python
from electric_car import ElectricCar as EC
```
## The Python standard library
The *Python standard library* is a set of modules included with every Python installation.
```python
form random import randint, choice

print(randint(1, 6))
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print(choice(players))
```
`choice()` takes in a list or tuple and returns a randomly chosen element.
## Styling classes
* Class names should be written in *CamelCase*.
* Every class should have a docstring immediately following the class definition.
* You can use blank lines to organize code, one between methods, and two to separate classes.
* Place the import statement for the standard library module first. Then add a blank line and the import statement for the module you wrote.
#### *Next*
[[09 - Files and exceptions]]