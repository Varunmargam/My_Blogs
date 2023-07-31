---
title: "Python: Empowering DevOps with Automation and Efficiency (Part 3)"
datePublished: Mon Jul 31 2023 18:22:53 GMT+0000 (Coordinated Universal Time)
cuid: clkr777uh000u0al8b8vkhuit
slug: python-empowering-devops-with-automation-and-efficiency-part-3
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690827720316/19135a32-f0de-455d-8d3c-6314882d7d3e.png
tags: python3, devops-journey, 90daysofdevops, day15, trainwithshubham

---

---

# Introduction

📚Welcome to Part 3 of the Python for DevOps Blog Series!🐍

In this blog, we will learn about Modules, Packages, Libraries, and File-Handling in Python. We will be learning Python from the basics to all the necessary things you will require for all your DevOps tasks. Let's unlock Python's potential in DevOps together!🌟

---

# Modules & Libraries

## Modules

Modules are a block consisting of Python code that has some functions, classes, and tasks written, and well-tested inside it. These modules come in very handy while writing a large codebase where you don't want to write every minute functionality from scratch. There are 2 types of modules in Python:

1. **Built-In Modules** - They are provided along with Python which contains various data structures and code blocks with various functionalities. Eg: os module, random module, math module, statistic module, time module, etc.
    
2. **External Modules** - These Modules are created by the people so that while writing Python code the developers can use the functions in these modules while creating large projects. They are to be downloaded externally using the `pip install <module_name>` command. Eg: flask, sklearn, matplotlib, etc.
    

You can use the modules by using the `import` command, type `import <module_name>` at the top of your Python code file.

It is not feasible to know all the functions provided by all the modules therefore, you can see the module's documentation from Google. You can also create your module inside a file with a `.py` extension.

(Photo)

# Package

Packages are folders that contain a collection of related modules. It contains an `init.py` file inside that makes the folder a Python package. You can import the modules from a package using the command `from <package_name> import <module_name>`.

# Libraries

Libraries in Python contain a collection of Python packages and modules. Libraries are very helpful for developing large-scale projects. Python has a large number of libraries useful for various fields making it popular for developing. Fields like Machine Learning, Data Science, Data visualization, DevOps, etc. Python is widely used.

```python
import <library_name> # To use libraries in Python
from <library> import <module_name> # To import a specific module from the library.
from <library> import * # To import all the modules inside the library.
```

Popular Python Libraries are:

1. NumPy: A library for numerical computing, linear algebra, and statistical operations providing support for arrays and matrices and numerous mathematical functions.
    
2. Pandas: A library for data manipulation and analysis, used for data visualization, statistical analysis, missing data handling, and offers data structures like DataFrames that make it easy to work with structured data.
    
3. Matplotlib: A powerful plotting library that enables the creation of various types of charts and visualizations, 3D plotting, and animations (animated visualizations).
    
4. TensorFlow and PyTorch: Libraries for machine learning and deep learning, offering tools to build and train neural networks.
    
5. Django and Flask: Web frameworks that simplify web development by providing tools for routing, templating, and handling requests.
    
6. os and shutil: Libraries for file and directory management, providing functionalities like file operations, path manipulation, and more.
    

---

# File Handling

Python has built-in file-handling functions. Here are some of the file-handling functions:

1. `open(<filename>, <operation>)`: It is used to open files inside Python. It takes in 2 arguments:
    
    * `<1st argument>` - filename (should be present inside the folder where your Python file resides)
        
    * `<2nd argument>` - which operation do you want to perform on the file it can be
        
        * read - `'r'`
            
        * write - `'w'` (it will overwrite the contents in the file)
            
        * append - `'a'` (it will add the text at the end of the content present in the file.
            
        * create - `'x'` (creates a file and throws an error if the file already exists)
            
    
    I will create a text file named `file.txt` and put some content in it.
    
    ```python
    f = open('file.txt', 'r') # This will open the file in read mode
    file_data = f.read() # It will read the content in the file and return it.
    print(file_data)
    f.close  # To close the opened file.
    ```
    
    Output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690824404556/a95c445d-74c1-44fb-b036-74b617778532.png align="center")
    
    ```python
    f = open('file.txt', 'w')
    f.write("This content is overwritten since this file was opened in the write mode.")
    f.close()
    ```
    
    After executing the above code you will see the content was written inside the file:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690824804786/9b9e1137-4593-4df9-b8f7-dd0366f0490c.png align="center")
    
2. `with`: It is another way to handle files this is more used since we have to write less.
    
    ```python
    with open('file.txt', 'a') as f:
        f.write("\nThis is an example to handle files using with statement.\nThis content will be appended to the existing content since the file is opened in the append mode.")
    # when we use with we do not need to close the file.
    # the indentation (space is important)
    # \n is used to print the content in the next line.
    ```
    
    Output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690825418214/b31e67c9-c040-4fbf-aee0-0b434d758262.png align="center")
    

---

# Reading a JSON file

To read a JSON file in Python we have to use an in-built module by doing:

`import json`

```json
{
    "services": {
      "debug": "on",
      "aws": {
        "name": "EC2",
        "type": "pay per hour",
        "instances": 500,
        "count": 500
      },
      "azure": {
        "name": "VM",
        "type": "pay per hour",
        "instances": 500,
        "count": 500
      },
      "gcp": {
        "name": "Compute Engine",
        "type": "pay per hour",
        "instances": 500,
        "count": 500
      }
    }
  }
```

Before we dive into how to read a JSON file, let's understand 2 methods/functions inside the JSON module, which will be very useful for reading the JSON file.

1. `loads()`: It converts the JSON string into a Python dictionary. JSON string means simply the above content in the JSON file has been put under a string using `''`. And this JSON string is given as a `<argument>` to the loads() function.
    
    ```python
    import json
    
    x = '{"name": "varun", "age": 21, "gender": "male"}' # This is a string
    # You can do print(type(x)) output will be <class 'str'>
    y = json.loads(x) # loads() is a method inside the json module.
    print(type(y))
    print(y)
    ```
    
    Output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690826598620/3d5c3d02-3902-4be4-92ce-c51034cc80db.png align="center")
    
2. `dumps()`: It is the opposite of `loads()`, `dumps()` converts a Python dictionary into a JSON file.
    
    ```python
    import json
    x = {"name": "varun", "age": 21, "gender": "male"}
    
    print(type(x))
    print(x)
    y = json.dumps(x)
    print(y)
    print(type(y)) # This will give string but it is a JSON string
    ```
    
    Output:
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690827045438/8511290d-b529-4b04-93db-3ace8b55ba8f.png align="center")
    

## Task:

Read the above JSON file and print the service names of every cloud service provider.

```python
import json # This is a built-in library in Python 

with open("services.json", 'r') as f:
    json_data = json.loads(f.read())
print(json_data)
print(type(json_data))
# f.read() will return the content in the JSON file
# json.loads() will convert the JSON content into a dictionary and will be stored in json_data.
# make sure that the above JSON file is inside the folder where this Python file resides
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690827461903/13e14061-01f4-4f94-a7d5-01f03b842692.png align="center")

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Python Playlist by TrainWithShubham](https://www.youtube.com/watch?v=bn-eH7BXyj4&list=PLlfy9GnSVerS_L5z0COaF7rsbgWmJXTOM&index=3)
    
* [JSON loads and dumps By TrainWithShubham](https://www.youtube.com/watch?v=Nc8au-99pfI)
    
* [Python playlist by CodeWithHarry](https://www.youtube.com/playlist?list=PLu0W_9lII9agwh1XjRt242xIpHhPT2llg)