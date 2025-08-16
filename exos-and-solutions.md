# Programming with Python — Exercises & Solutions

---

## Exercise 1: Working with Lists

**Task:**
Using the following list:
```python
my_list = [1, 2, 2, 4, 4, 5, 6, 8, 10, 13, 22, 35, 52, 83]
```

Write a program that:
- Prints out all the elements of the list that are higher than or equal to 10
- Instead of printing the elements one by one, make a new list that has all the elements higher than or equal to 10 from this list in it and print out this new list
- Ask the user for a number as input and print a list that contains only those elements from my_list that are higher than the number given by the user

**Solution:**

```python
# Print out elements higher than or equal to 10
my_list = [1, 2, 2, 4, 4, 5, 6, 8, 10, 13, 22, 35, 52, 83]
for number in my_list:
    if number >= 10:
        print(number)

# Make a new list with all elements higher than or equal to 10 and print it out
my_list = [1, 2, 2, 4, 4, 5, 6, 8, 10, 13, 22, 35, 52, 83]
my_new_list = []
for number in my_list:
    if number >= 10:
        my_new_list.append(number)
print(my_new_list)

# User input as a number and print a list that contains only those elements from my_list that are higher than the number given by the user
user_input = input("Enter a number: ")
my_list = [1, 2, 2, 4, 4, 5, 6, 8, 10, 13, 22, 35, 52, 83]
my_new_list = []
for number in my_list:
    if number > int(user_input):
        my_new_list.append(number)
print(my_new_list)
```

---

## Exercise 2: Working with Dictionaries

**Task:**
Using the following dictionary:
```python
employee = {
  "name": "Tim",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer"
}
```

Write a Python Script that:
- Updates the job to Software Engineer
- Removes the age key from the dictionary
- Loops through the dictionary and prints the key:value pairs one by one

Using the following 2 dictionaries:
```python
dict_one = {'a': 100, 'b': 400} 
dict_two = {'x': 300, 'y': 200}
```

Write a Python Script that:
- Merges these two Python dictionaries into 1 new dictionary
- Sums up all the values in the new dictionary and prints it out
- Prints the max and minimum values of the dictionary

**Solution:**

**Working with one dictionary:**
```python
# Update the job to Software Engineer
employee = {
  "name": "Tim",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer"
}

employee["job"] = "Software Engineer"
print(employee)

# Remove the age key from the dictionary
employee = {
  "name": "Tim",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer"
}

employee.pop("age")
print(employee)

# Loop through the dictionary and print the key:value pairs one by one
employee = {
  "name": "Tim",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer"
}

for key, value in employee.items():
  print(f"{key}:{value}")
```

**Working with multiple dictionaries:**
```python
# Merge these two Python dictionaries into 1 new dictionary
dict_one = {'a': 100, 'b': 400} 
dict_two = {'x': 300, 'y': 200}

dict_merged = dict_one.copy()
dict_merged.update(dict_two) 
print(dict_merged)

# Sum up all the values in the new dictionary and print it out
dict_one = {'a': 100, 'b': 400} 
dict_two = {'x': 300, 'y': 200}

dict_merged = dict_one.copy()
dict_merged.update(dict_two) 

sum_of_values = 0
for value in dict_merged.values():
    sum_of_values = sum_of_values + value
print(sum_of_values)

# Print the max and minimum values of the dictionary
dict_one = {'a': 100, 'b': 400} 
dict_two = {'x': 300, 'y': 200}

dict_merged = dict_one.copy()
dict_merged.update(dict_two)

merged_values = []
for value in dict_merged.values():
    merged_values.append(value)

merged_values.sort()
print(f"min value: {merged_values[0]}")
print(f"max value: {merged_values[len(merged_values)-1]}")
```

---

## Exercise 3: Working with List of Dictionaries

**Task:**
Using a list of 2 dictionaries:
```python
employees = [{
  "name": "Tina",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer",
  "address": {
    "city": "New York",
    "country": "USA"
  }
},
{
  "name": "Tim",
  "age": 35,
  "birthday": "1985-02-21",
  "job": "Developer",
  "address": {
    "city": "Sydney",
    "country": "Australia"
  }
}]
```

Write a Python Program that:
- Prints out - the name, job and city of each employee using a loop. The program must work for any number of employees in the list, not just 2
- Prints the country of the second employee in the list by accessing it directly without the loop

**Solution:**

```python
# Print out - the name, job and city of each employee using a loop. The program must work for any number of employees in the list, not just 2
employees = [{
  "name": "Tina",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer",
  "address": {
    "city": "New York",
    "country": "USA"
  }
},
{
  "name": "Tim",
  "age": 35,
  "birthday": "1985-02-21",
  "job": "Developer",
  "address": {
    "city": "Sydney",
    "country": "Australia"
  }
}]

for employee in employees:
    print(f"name: {employee['name']}")
    print(f"job: {employee['job']}")
    print(f"city: {employee['address']['city']}")
    print("-----------------------")

# Prints the country of the second employee in the list by accessing it directly without the loop
country = employees[1]["address"]["country"]
print(f"country of the second employee: {country}")
```

---

## Exercise 4: Working with Functions

**Task:**
- Write a function that accepts a list of dictionaries with employee age (see example list from Exercise 3) and prints out the name and age of the youngest employee
- Write a function that accepts a string and calculates the number of upper case letters and lower case letters
- Write a function that prints the even numbers from a provided list
- For cleaner code, declare these functions in its own helper Module and use them in the main.py file

**Solution:**

**Functions in main.py:**
```python
# Write a function that accepts a list of dictionaries with employee age and prints out the name and age of the youngest employee
employees = [{
  "name": "Tina",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer",
  "address": {
    "city": "New York",
    "country": "USA"
  }
},
{
  "name": "Tim",
  "age": 35,
  "birthday": "1985-02-21",
  "job": "Developer",
  "address": {
    "city": "Sydney",
    "country": "Australia"
  }
}]

def print_employee_info(employees):
    youngest_employee_age = employees[0]["age"]
    youngest_employee_name = employees[0]["name"]
    for employee in employees:
        if employee["age"] < youngest_employee_age:
            youngest_employee_age = employee["age"]
            youngest_employee_name = employee["name"]

    print(f"name of the youngest employee: {youngest_employee_name}")
    print(f"age of the youngest employee: {youngest_employee_age}")

print_employee_info(employees)

# Write a function that accepts a string and calculates the number of upper case letters and lower case letters
def count_upper_and_lower_letters(string):
    lower_letters = 0
    upper_letters = 0
    for char in list(string):
        if char.islower():
            lower_letters += 1
        elif char.isupper():
            upper_letters += 1
    print(f"number of lower case letters: ", lower_letters)
    print(f"number of upper case letters: ", upper_letters)

count_upper_and_lower_letters("sWWbb137WATbfgdbWb")

# Write a function that prints the even numbers from a provided list
def print_even_numbers(numbers_list):
    for number in numbers_list:
        if number % 2 == 0:
            print(number)

print_even_numbers([0, 3, 9, 10, 2, 13, 120])
```

**Function in helper module:**

For cleaner code, declare these functions in its own helper Module and use them in the main.py file

**helper.py:**
```python
def print_employee_info(employees):
    youngest_employee_age = employees[0]["age"]
    youngest_employee_name = employees[0]["name"]
    for employee in employees:
        if employee["age"] < youngest_employee_age:
            youngest_employee_age = employee["age"]
            youngest_employee_name = employee["name"]

    print(f"name of the youngest employee: {youngest_employee_name}")
    print(f"age of the youngest employee: {youngest_employee_age}")

def count_upper_and_lower_letters(string):
    lower_letters = 0
    upper_letters = 0
    for char in list(string):
        if char.islower():
            lower_letters += 1
        elif char.isupper():
            upper_letters += 1
    print(f"number of lower case letters: ", lower_letters)
    print(f"number of upper case letters: ", upper_letters)

def print_even_numbers(numbers_list):
    for number in numbers_list:
        if number % 2 == 0:
            print(number)
```

**main.py:**
```python
from helper import print_employee_info, count_upper_and_lower_letters, print_even_numbers

employees = [{
  "name": "Tina",
  "age": 30,
  "birthday": "1990-03-10",
  "job": "DevOps Engineer",
  "address": {
    "city": "New York",
    "country": "USA"
  }
},
{
  "name": "Tim",
  "age": 35,
  "birthday": "1985-02-21",
  "job": "Developer",
  "address": {
    "city": "Sydney",
    "country": "Australia"
  }
}]

print_employee_info(employees)
count_upper_and_lower_letters("sWWbb137WATbfgdbWb")
print_even_numbers([0, 3, 9, 10, 2, 13, 120])
```

---

## Exercise 5: Python Program 'Calculator'

**Task:**
Write a simple calculator program that:
- Takes user input of 2 numbers and operation to execute
- Handles the following operations: plus, minus, multiply, divide
- Does proper user validation and give feedback: only numbers allowed
- Keeps the Calculator program running until the user types "exit"
- Keeps track of how many calculations the user has taken, and when the user exits the calculator program, prints out the number of calculations the user did

*Concepts covered: working with different data types, conditionals, type conversion, user input, user input validation*

**Solution:**

```python
def calculator(number1, number2, operation):
    # from Python version 3.10, you can use match-case
    if operation == "plus":
        print(number1 + number2)
    elif operation == "minus":
        print(number1 - number2)
    elif operation == "multiply":
        print(number1 * number2)
    elif operation == "divide":
        print(number1 / number2)

number_of_calculations_done = 0 
while True:
    number1 = input("Enter the first number: ")

    if number1 == "exit":
        print("exiting the program")
        print(f"you did {number_of_calculations_done} calculations")
        break

    number2 = input("Enter the second number: ")
    operation = input("What operation do you want to perform on these numbers (plus, minus, multiply, divide): ")

    valid_numbers = number1.isnumeric() and number2.isnumeric()
    valid_operation = operation == "plus" or operation == "minus" or operation == "multiply" or operation == "divide"
    if not valid_numbers:
        print("only numbers allowed") 
    elif not valid_operation:
        print("operation not supported")
    else:
        calculator(int(number1), int(number2), operation)
        number_of_calculations_done += 1
```

---

## Exercise 6: Python Program 'Guessing Game'

**Task:**
Write a program that:
- Runs until the user guesses a number (hint: while loop)
- Generates a random number between 1 and 9 (including 1 and 9)
- Asks the user to guess the number
- Then prints a message to the user, whether they guessed too low, too high
- If the user guesses the number right, print out YOU WON! and exit the program

*Hint: Use the built-in random module to generate random numbers https://docs.python.org/3/library/random.html*

*Concepts covered: Built-In Module, User Input, Comparison Operator, While loop*

**Solution:**

```python
from random import randint

while True:
    number_to_guess = randint(1, 19)
    users_guess = int(input("Guess the number: "))

    if users_guess == number_to_guess:
        print("YOU WON!")
        break

    elif users_guess < number_to_guess:
        print("You guessed too low")

    elif users_guess > number_to_guess:
        print("You guessed too high")
```

---

## Exercise 7: Working with Classes and Objects

**Task:**
Imagine you are working in a university and need to write a program, which handles data of students, professors and lectures. To work with this data you create classes and objects:

a) **Create a Student class** with properties: first name, last name, age, lectures they attend
   with methods: can print the full name, can list the lectures, can add new lectures, can remove lectures

b) **Create a Professor class** with properties: first name, last name, age, subjects they teach
   with methods: can print the full name, can list the subjects, can add new subjects, can remove subjects

c) **Create a Lecture class** with properties: name, max number of students, duration, list of professors
   with methods: printing the name and duration, adding professors to the list

d) **Bonus task:** Create a Person class as parent class for Student and Professor classes with inheritance

**Solution:**

**lecture.py:**
```python
class Lecture:
    def __init__(self, name, max_students, duration, professors):
        self.name = name
        self.max_students = max_students
        self.duration_minutes = duration
        self.professors = professors
    
    def print_name_and_duration(self):
        print(f"{self.name} - {self.duration_minutes} minutes")

    def add_professors(self, new_professor):
        self.professors.append(new_professor)
```

**person.py (Parent class):**
```python
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
    
    def print_full_name(self):
        print(f"{self.first_name} {self.last_name}")
```

**professor.py:**
```python
from person import Person

class Professor(Person):
    def __init__(self, first_name, last_name, age, lectures):
        super().__init__(first_name, last_name, age)
        self.lectures = lectures

    def list_lectures(self):
        print("Teaches lectures:")
        for lecture in self.lectures:
            print(f"- {lecture.name}")
    
    def teach_lecture(self, new_lecture):
        self.lectures.append(new_lecture)

    def remove_lecture(self, lecture):
        self.lectures.pop(lecture)
```

**student.py:**
```python
from person import Person

class Student(Person):
    def __init__(self, first_name, last_name, age, lectures):
        super().__init__(first_name, last_name, age)
        self.lectures = lectures
    
    def list_lectures(self):
        print("Attends lectures:")
        for lecture in self.lectures:
            print(f"- {lecture.name}")

    def attend_lecture(self, new_lecture):
        self.lectures.append(new_lecture)

    def leave_lecture(self, lecture):
        self.lectures.pop(lecture)
```

**main.py (Test your code):**
```python
from professor import Professor
from student import Student
from lecture import Lecture

cs_lecture = Lecture("Computer science", 15, 45, [])
python_basics_lecture = Lecture("Python programming basics", 25, 90, [])
python_advanced_lecture = Lecture("Python advanced", 10, 90, [])
algorithms_lecture = Lecture("Algorithms and data structures", 30, 120, [])

new_professor = Professor("Maria", "Smith", 34, [cs_lecture, python_basics_lecture])
new_professor.print_full_name()
new_professor.teach_lecture(python_advanced_lecture)
new_professor.list_lectures()

cs_lecture.add_professors(new_professor)
python_basics_lecture.add_professors(new_professor)
python_advanced_lecture.add_professors(new_professor)

print("------------------------------")

new_student = Student("David", "Green", 25, [algorithms_lecture])
new_student.print_full_name()
new_student.attend_lecture(python_basics_lecture)
new_student.list_lectures()

print("------------------------------")

cs_lecture.print_name_and_duration()
python_basics_lecture.print_name_and_duration()
```

---

## Exercise 8: Working with Dates

**Task:**
Write a program that:
- Accepts user's birthday as input
- And calculates how many days, hours and minutes are remaining till the birthday
- Prints out the result as a message to the user

**Solution:**

```python
from datetime import datetime

birthday_string = input("Enter your birthday (example - 20/09/2000): ")

birthday_date = datetime.strptime(birthday_string, '%d/%m/%Y').date()
today = datetime.today()

difference_one = datetime(today.year, birthday_date.month, birthday_date.day)
difference_two = datetime(today.year + 1, birthday_date.month, birthday_date.day)

days_till_birthday = 0
if difference_one > today:
    # birthday this year
    days_till_birthday = difference_one - today
else:
    # birthday next year
    days_till_birthday = difference_two - today   

print(f"{days_till_birthday.days} days till your birthday")
```

---

## Exercise 9: Working with Spreadsheets

**Task:**
Write a program that:
- Reads the provided spreadsheet file "employees.xlsx" with the following information/columns: "name", "years of experience", "job title", "date of birth"
- Creates a new spreadsheet file "employees_sorted.xlsx" with following info/columns: "name", "years of experience", where the years of experience is sorted in descending order: so the employee name with the most experience in years is on top

**Solution:**

```python
import openpyxl
from operator import itemgetter

empl_file = openpyxl.load_workbook("employees.xlsx")
empl_list = empl_file["Sheet1"]

# remove columns 3 and 4
empl_list.delete_cols(3,4)

employees_by_experience = []

for empl_row in range(2, empl_list.max_row + 1):
    empl_name = empl_list.cell(empl_row, 1).value
    empl_experience = empl_list.cell(empl_row, 2).value

    employees_by_experience.append({ 
        "name":  empl_name, 
        "experience": int(empl_experience)
    })

# sort the list of dictionaries by experience
new_list = sorted(employees_by_experience, key=itemgetter("experience"), reverse=True)

# add entries to the spreadsheet sorted by experience
for empl_row in range(2, empl_list.max_row + 1):
    empl_name = empl_list.cell(empl_row, 1)
    empl_experience = empl_list.cell(empl_row, 2)

    # because the rows start from row 2, but index for our list starts at 0
    index = empl_row - 2
    employee = new_list[index]

    empl_name.value = employee["name"]
    empl_experience.value = employee["experience"]

empl_file.save("employees_sorted_by_experience.xlsx")
```

*NOTE: there are also other libraries for working with spreadsheets, which enable you to sort and filter columns, this is just one way of doing it*

---

## Exercise 10: Working with REST APIs

**Task:**
Write a program that:
- Connects to GitHub API
- Gets all the public repositories for a specific GitHub user
- Prints the name & URL of every project

**Solution:**

```python
import requests

# replace with your own user 
user = "techworld-with-nana"
response = requests.get(f"https://api.github.com/users/{user}/repos")
my_projects = response.json()

# print just the names and urls
for project in my_projects:
    print(f"Project Name: {project['name']}\nProject Url: {project['html_url']}\n")
```
