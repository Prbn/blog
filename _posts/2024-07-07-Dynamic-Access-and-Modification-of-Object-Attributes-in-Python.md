# Dynamic Access and Modification of Object Attributes in Python

Code:

<a href="https://colab.research.google.com/drive/1oSTMYFMHq0Y60SR-IzLYiS78nFpEvrlP"
  target="_parent">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="To run open In Colab"/>
</a>

---

Written By:
[Prabin Raj Shrestha](mailto:prabin.r.shrestha@gmail.com)

pshres01@syr.edu | [linkedin.com/in/prbnrs](linkedin.com/in/prbnrs) | [github.com/Prbn](github.com/Prbn)

<a href="https://www.linkedin.com/in/prbnrs/" target="_blank">
  <img src="https://content.linkedin.com/content/dam/me/business/en-us/amp/brand-site/v2/bg/LI-Bug.svg.original.svg"
  alt="LinkedIn of Prabin Raj Shrestha"
  width="100" height="100"/>
</a>
<a href="https://github.com/Prbn/Profile/blob/main/README.md" target="_blank">
  <img src="https://raw.githubusercontent.com/gilbarbara/logos/29e8719bf78915c7a82a26a6c203f53c4cb8fff2/logos/github.svg"
  alt="GitHub of Prabin Raj Shrestha"
  width="200" height="100"/>
</a>

---



## Introduction
In this notebook, we'll learn how to dynamically access and change object attributes during runtime in Python

There are four functions in Python that allow us to dynamically access and change attributes of objects during runtime:
1. `getattr()`
2. `setattr()`
3. `hasattr()`
4. `delattr()`


```python
# Simple class example
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

### Creating and Printing an Object
Let's create a `Person` object and print its attributes.


```python
p = Person("Raj", 25)
print(p.name)  # Output: Raj
print(p.age)   # Output: 25
```

    Raj
    25


### Dynamic Access in Data Structures
In pandas, we can access DataFrame columns dynamically using dictionary-like syntax. This idea can be extended to class attributes.


```python
import pandas as pd

# Example DataFrame
df = pd.DataFrame({'column_name': [1, 2, 3]})
print(df['column_name'])  # Dynamic column access in pandas
```

    0    1
    1    2
    2    3
    Name: column_name, dtype: int64


## Dynamic Attribute Access
Unlike dictionaries, you can't dynamically access class attributes using subscript notation. For dynamic access, we can use the `getattr` function.

we can use `getattr()` to dynamically access attributes during runtime based on user input or certain conditions.

The `setattr()` function allows us to dynamically set the attributes of an object. This is useful when the attribute name and value are determined at runtime.


Syntax: `getattr(object, attribute_name, default_value)`

- `object`: The object from which you want to get the attribute.
- `attribute_name`: The name of the attribute you want to access.
- `default_value`: The value to return if the attribute does not exist (optional).



```python
# @title Example: Access Attribute

# choice = input("Which attribute do you want to access? ")
choice = "name" # For example, user wants to access 'name'

print(getattr(p, choice, 'Non-existent'))
```

    Raj


## Dynamic Attribute Setting
We can also dynamically set attributes using the `setattr` function.

Syntax: `setattr(object, attribute_name, value)`

- `object`: The object on which you want to set the attribute.
- `attribute_name`: The name of the attribute you want to set.
- `value`: The value to set for the attribute.


```python
# @title Example: Set Attribute

# choice = input("Which attribute do you want to change? ")
# value = input("What do you want to change this to? ")

choice = "name"  # For example, user wants to change 'name'
new_value = "Aman"  # New value for the attribute

setattr(p, choice, new_value)

print(f"{choice} has been set to {new_value}")
```

    name has been set to Aman


### Creating New Attributes
You can even create new attributes dynamically.


```python
# @title Example: Set New Attribute

# new_att_name = input("New Attribute Name: ")
# new_att_value = input("New Attribute Value: ")

new_att_name = 'height'
new_att_value = 180

setattr(p, new_att_name, new_att_value)


print(getattr(p, new_att_name, new_att_value)) # Output: 180
```

    180


## Checking Attributes

For checking attributes we can use the function `hasattr`

The `hasattr()` function allows us to check if an attribute exists in an object. This is useful for validating the existence of an attribute before performing operations on it.

Syntax: `hasattr(object, attribute_name)`

- `object`: The object on which you want to check the attribute.
- `attribute_name`: The name of the attribute to check.


```python
# @title Example: Checking Attribute

# choice = input("Which attribute do you want to check? ")

choice = "age"  # For example, user wants to check if 'age' exists
exists = hasattr(p, choice)
print(f"Attribute '{choice}' exists: {exists}")
```

    Attribute 'age' exists: True


## Deleting Attributes

For deleting attributes we can use the function `delattr`

The `delattr()` function allows us to delete an attribute from an object. This is useful when you need to remove attributes dynamically.

Syntax: `delattr(object, attribute_name)`

- `object`: The object from which you want to delete the attribute.
- `attribute_name`: The name of the attribute to delete.


```python
# @title Example: Deleting Attribute

# choice = input("Which attribute do you want to check? ")

choice = "age"  # For example, user wants to delete 'age'
if hasattr(p, choice):
    delattr(p, choice)
    print(f"Deleted attribute '{choice}'")
else:
    print(f"Attribute '{choice}' does not exist")
```

    Deleted attribute 'age'


We demonstrated how to dynamically access and modify object attributes in Python using `getattr()`, `setattr()`, `hasattr()`, and `delattr()`. These functions provide flexibility for handling object attributes based on runtime conditions, user input, or other dynamic sources.

That's how you can dynamically get, set, check, and delete attributes in Python during runtime.

---

---
---
