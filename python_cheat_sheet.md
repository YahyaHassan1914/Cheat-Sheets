# Python Advanced Cheat Sheet

## 1. **Basic Syntax**

- **Print to Console**:
  ```python
  print("Hello, World!")
  ```

- **Comments**:
  ```python
  # Single line comment
  """
  Multi-line comment
  """
  ```

- **Data Types**:
  ```python
  int_var = 10          # Integer
  float_var = 10.5      # Float
  str_var = "Hello"     # String
  bool_var = True       # Boolean
  ```

- **String Formatting**:
  ```python
  name = "John"
  age = 30

  # f-strings (Python 3.6+)
  print(f"My name is {name} and I am {age} years old.")

  # format method
  print("My name is {} and I am {} years old.".format(name, age))

  # % operator
  print("My name is %s and I am %d years old." % (name, age))
  ```

## 2. **Control Structures**

- **If Statements**:
  ```python
  if x > 10:
      print("x is greater than 10")
  elif x == 10:
      print("x is 10")
  else:
      print("x is less than 10")
  ```

- **For Loops**:
  ```python
  for i in range(5):
      print(i)

  # Iterate over a list
  for item in [1, 2, 3]:
      print(item)
  ```

- **While Loops**:
  ```python
  count = 0
  while count < 5:
      print(count)
      count += 1
  ```

- **List Comprehensions**:
  ```python
  squares = [x**2 for x in range(10)]
  ```

- **Lambda Functions**:
  ```python
  square = lambda x: x**2
  print(square(5))
  ```

## 3. **Functions**

- **Defining Functions**:
  ```python
  def greet(name):
      return f"Hello, {name}!"

  print(greet("Alice"))
  ```

- **Default Arguments**:
  ```python
  def greet(name="World"):
      return f"Hello, {name}!"
  ```

- **Variable-Length Arguments**:
  ```python
  def sum_numbers(*args):
      return sum(args)
  ```

- **Keyword Arguments**:
  ```python
  def describe_person(name, **kwargs):
      print(f"Name: {name}")
      for key, value in kwargs.items():
          print(f"{key}: {value}")
  ```

## 4. **Classes and Objects**

- **Defining Classes**:
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name
          self.age = age

      def greet(self):
          return f"Hello, my name is {self.name} and I am {self.age} years old."
  ```

- **Inheritance**:
  ```python
  class Student(Person):
      def __init__(self, name, age, student_id):
          super().__init__(name, age)
          self.student_id = student_id

      def greet(self):
          return f"Student ID: {self.student_id}, " + super().greet()
  ```

## 5. **Modules and Packages**

- **Importing Modules**:
  ```python
  import math
  from math import sqrt
  ```

- **Creating a Module**:
  ```python
  # my_module.py
  def say_hello():
      return "Hello!"
  ```

  ```python
  # main.py
  import my_module
  print(my_module.say_hello())
  ```

- **Installing Packages**:
  ```sh
  pip install <package_name>
  ```

## 6. **File Handling**

- **Reading a File**:
  ```python
  with open('file.txt', 'r') as file:
      content = file.read()
  ```

- **Writing to a File**:
  ```python
  with open('file.txt', 'w') as file:
      file.write("Hello, World!")
  ```

- **Appending to a File**:
  ```python
  with open('file.txt', 'a') as file:
      file.write("Appending some text.")
  ```

## 7. **Exception Handling**

- **Try/Except**:
  ```python
  try:
      result = 10 / 0
  except ZeroDivisionError:
      print("Cannot divide by zero!")
  finally:
      print("Execution finished.")
  ```

## 8. **Advanced Data Structures**

- **Sets**:
  ```python
  my_set = {1, 2, 3}
  my_set.add(4)
  my_set.remove(1)
  ```

- **Dictionaries**:
  ```python
  my_dict = {"key1": "value1", "key2": "value2"}
  my_dict["key3"] = "value3"
  ```

- **Named Tuples**:
  ```python
  from collections import namedtuple

  Person = namedtuple('Person', ['name', 'age'])
  person = Person(name="Alice", age=30)
  ```

## 9. **Decorators**

- **Function Decorator**:
  ```python
  def decorator_function(original_function):
      def wrapper_function():
          print("Wrapper executed")
          return original_function()
      return wrapper_function

  @decorator_function
  def say_hello():
      return "Hello!"
  ```

- **Class Decorator**:
  ```python
  def add_method(cls):
      cls.new_method = lambda self: "New method"
      return cls

  @add_method
  class MyClass:
      pass
  ```

## 10. **Generators and Iterators**

- **Generator Functions**:
  ```python
  def count_up_to(max):
      count = 1
      while count <= max:
          yield count
          count += 1
  ```

- **Using Generators**:
  ```python
  for num in count_up_to(5):
      print(num)
  ```

## 11. **Concurrency**

- **Threading**:
  ```python
  import threading

  def print_numbers():
      for i in range(5):
          print(i)

  thread = threading.Thread(target=print_numbers)
  thread.start()
  ```

- **Asyncio**:
  ```python
  import asyncio

  async def say_hello():
      await asyncio.sleep(1)
      print("Hello")

  asyncio.run(say_hello())
  ```

## 12. **Data Analysis with Pandas**

- **Basic DataFrame Operations**:
  ```python
  import pandas as pd

  df = pd.DataFrame({
      'A': [1, 2, 3],
      'B': [4, 5, 6]
  })

  print(df.head())
  ```

- **Reading and Writing Data**:
  ```python
  df.to_csv('file.csv')
  df = pd.read_csv('file.csv')
  ```

## 13. **Web Development**

- **Flask Basic Example**:
  ```python
  from flask import Flask

  app = Flask(__name__)

  @app.route('/')
  def home():
      return "Hello, Flask!"

  if __name__ == "__main__":
      app.run()
  ```

- **FastAPI Basic Example**:
  ```python
  from fastapi import FastAPI

  app = FastAPI()

  @app.get("/")
  def read_root():
      return {"Hello": "World"}
  ```

## 14. **Testing**

- **Unit Testing with Unittest**:
  ```python
  import unittest

  class TestStringMethods(unittest.TestCase):
      def test_upper(self):
          self.assertEqual('foo'.upper(), 'FOO')

  if __name__ == '__main__':
      unittest.main()
  ```

- **Testing with Pytest**:
  ```python
  def test_addition():
      assert 1 + 1 == 2
  ```

## 15. **Virtual Environments**

- **Create a Virtual Environment**:
  ```sh
  python -m venv myenv
  ```

- **Activate the Virtual Environment**:
  - **Windows**: 
    ```sh
    myenv\Scripts\activate
    ```
  - **Unix/MacOS**: 
    ```sh
    source myenv/bin/activate
    ```

- **Deactivate the Virtual Environment**:
  ```sh
  deactivate
  ```

---

This cheat sheet covers the essential and advanced aspects of Python, from basic syntax and data structures to web development, concurrency, and testing. For further information, you can refer to the [official Python documentation](https://docs.python.org/3/).