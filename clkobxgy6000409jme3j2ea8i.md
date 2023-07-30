---
title: "Python: Empowering DevOps with Automation and Efficiency (Part 1)"
datePublished: Sat Jul 29 2023 18:11:58 GMT+0000 (Coordinated Universal Time)
cuid: clkobxgy6000409jme3j2ea8i
slug: python-empowering-devops-with-automation-and-efficiency-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690739842144/d3c9c74e-b682-47c0-a835-b4809db981b1.png
tags: python, devops-journey, 90daysofdevops, day13, trainwithshubham

---

---

# 📍Introduction

📚Welcome to Part 1 of my Python for DevOps Blog Series!🐍

Python is vital in DevOps for automation & integration. Python's flexibility and rich libraries make it robust across various fields, including DevOps. We will be learning Python from the basics to all the necessary things you will require for all your DevOps tasks. Let's unlock Python's potential in DevOps together!🌟

---

# 📍Data Types & Variables

## ✔Variables

Variables are the container that stores any value. These values can be of any data type. Eg: `a = 10`, here, a is a variable that stores the value `10`. We gave a name to the value so that we can perform operations on it.

Points to remember while naming your variable:

* Variables can contain alphabets, numbers, and underscores.
    
* A variable name can only start with an alphabet (small or capital), and an underscore, it cannot start with a number.
    
* No spaces are allowed between the variable names.
    

## ✔Data Types

**There are 2 types of Data Types in Python**:

* **Primitive Data Types**: Smallest type of data that cannot be broken down further.
    
    1. `Integers (int)`: Whole numbers negative or positive. Eg: 0, 1, -5, -6, etc.
        
    2. `Float (float)`: Decimal numbers negative or positive. Eg: 10.5, -11.2, 0.2, 10.0, etc.
        
    3. `String (str)`: Series or sequence of Characters or Alphabets. Eg: `"Varun Margam"`, `'Python3'`, `'1'`, etc. In Python, the characters or alphabets that are in `" "` is a string.
        
    4. `Boolean (bool)`: True or False.
        
* **Non-Primitive Data Types**: These are built using primitive data types.
    
    1. `Tuple`
        
    2. `Array`
        
    3. `List`
        
    4. `Dictionary`
        
    5. `Set`
        

(In my future blogs, we will be learning about these data types in detail, in this blog we will explore primitive data types.)

## ✔Hands-on - Primitive Data Types.

In Python, there is no need to define the type of data the variable is going to store. Based on the value Python dynamically identifies which data type is stored in the variable.

You can use the `print()` statement to print anything in Python. To see the type of variable use `print(type(variable))`. This will print the type of value stored in the variable.

```python
a = 10
print(a)
print(type(a))
```

When you run this simple Python program the output will be:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690639157722/8149bc77-63ee-4d5c-9b65-663e914ea474.png align="center")

As we can see the output of print(a) is 10 and of print(type(a)) is &lt;class 'int'&gt; i.e. a is storing a value of Integer data type.

Similarly, you can execute the following Python code and see the output for yourself.

```python
name = "Varun Margam"
percentage = 90.4
Is_raining = True

print(type(name))
print(type(percentage))
print(type(Is_raining))

print("My name is ",name)
#OR
print("My percentage is "+percentage)
#In this way you can print the variables with the printable text.
```

### ✔Comments

You can write comments inside the Python file using `#`. These comments are ignored by Python and are not executed. Comments are used to explain the code to make understand the code better (useful for organizing large codebases).

---

# 📍Operators

These are some commonly used operators in Python:

| Arithmetic Operators (used to perform arithmetic operations) | Assignment Operators (used to assign a value) | Comparison Operators (used to compare two values) | Logical Operators (used to combine two conditional statements) | Bitwise Operators (used to perform bitwise (binary) operations) |
| --- | --- | --- | --- | --- |
| Addition `+` | Equals `=` | Compares if Equal `==` | `and` (returns true if both the conditional statements are true) | AND `&` |
| Subtraction `-` | `+=` (`a += 3` i.e. `a = a+3`) | Not Equal `!=` | `or` (returns true if any one condition statement is true) | OR \` |
| Multiplication `*` | `-=` | Greater than `>` | `not` (reverse the result) | NOT `~` |
| Division `/` | `*=` | Less than `<` |  | XOR `^`, etc. |
| Modulus (remainder) `%`, etc. | `/=` ,etc. | `>=`, etc. |  |  |

Don't worry, a DevOps engineer doesn't need to know about all these operators only some of them will be frequently useful to us.

## ✔Hands-on Operators

```python
a = 10
b = 5
print(a + b) # Output: 15
print(a - b) # Output: 5
print(a * b) # Output: 50
print(a / b) # Output: 2  10/5 (Quotient)
print(a % b) # Output: 0 since 10 is divisible by 5 hence the remainder is 0
```

---

# 📍Type Casting

Type Casting is a method to convert the variable's data type into another data type. Type Casting can be done in two ways:

* **Explicit Type Casting**
    
* **Implicit Type Casting**
    

## ✔Explicit Type Casting

Here, you convert the data type of the value stored in the variable into another data type by explicitly mentioning it to Python.

* Int(): This is used to convert a float or a String( i.e. only numbers stored in `" "`) into an Integer i.e. &lt;class 'int'&gt;.
    
* float(): This is used to convert an Integer or a String( i.e. only numbers stored in `" "`) into a float i.e. &lt;class 'float'&gt;.
    
* str(): This is used to convert a float or an Integer into a String i.e. &lt;class 'str'&gt;.
    

```python
a = 10
a = float(a)
print(type(a))
a = str(a)
print(type(a))

str = "1101"
str = int(str)
print(type(str))
str = float(str)
print(type(str))
```

---

# 📍Input

Input from the user in Python can be taken using the `input()` function. It takes the input as a string. The output of the user's input will always be string irrespective of is the user entered integer or float.

```python
name = input("Enter your name: ")
print("Good Morning, ",name)

number = input("Enter any number: ")
print(type(number)) #The type of the output of user's input is always string.
```

---

# 📍Strings

The string in Python can be written in three ways:

```python
a = "Varun Margam"
a = 'Varun Margam'
a = '''Varun Margam''' #generally used when we write multiple lines a para"
a = 'V' # a single character is also a string usually is presented in ''.
```

The string stored in Python can be visualized as:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690646526169/446ea93f-012f-4d41-b4d8-50a26574683a.png align="center")

In the image you can see the string "Varun" is a sequence of characters where each character is stored in an index starting from 0 to 4. If the length of the string is n then the indexing of the characters will be starting from 0 till n-1. You can access the characters of the string using these indexes. For example:

```python
str = "Varun"
print(str[0]," ",str[1]," ",str[2]," ",str[3]," ",str[4])
#you cannot access str[5] as it does not exist Python will throw an Index OutOfBound Error
```

Run this code and see the output.

## ✔String Slicing

Syntax to slice a string is:

`variable = str_variable[start_index:end_index:skip_value]`

```python
str = "Varun"
slice = str[0:5]
#[start:end] means it will give the string from the start index to the end-1 index.
print(slice) # Output - Varun from 0th index to 4th index

print(str[0:3]) # Output - Var
print(str[0:]) # Output - Varun, if kept empty it will go till the last index same for [:5]
print(str[0:5:2]) # Output - Vrn, for [start:end:skip] it will skip the 'skip-1' letter.
print(str[::1]) #Output - Varun
```

## ✔String Functions

Some of the commonly used string functions:

1. `len("string" or "string_variable")`: Gives the length of the `string` i.e. the number of characters the `string` contains.
    
2. `string.capitalize()`: the given converts the first character to an upper case `string`.
    
3. `string.count(character)`: Returns the number of occurrences of a `character` in the `string`.
    
4. `string.find(word)`: Returns the index of the `word` in the `string`.
    
5. `string.replace(old_word,new_word)`: Replaces the `old_word` with the `new_word` in the entire `string`.
    

```python
str = "varun"
print(len(str)) 
print(str.capitalize())
print(str.count('a'))
print(str.count("run"))
print(str.replace("run","riable"))
```

Explore more string functions and get familiar with them.

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Python Playlist by TrainWithShubham](https://www.youtube.com/watch?v=bn-eH7BXyj4&list=PLlfy9GnSVerS_L5z0COaF7rsbgWmJXTOM&index=3)
    
* [Operators W3School](https://www.w3schools.com/python/python_operators.asp)
    
* [Python playlist by CodeWithHarry](https://www.youtube.com/playlist?list=PLu0W_9lII9agwh1XjRt242xIpHhPT2llg)
    

---