---
title: "Python: Empowering DevOps with Automation and Efficiency (Part 2)"
datePublished: Sun Jul 30 2023 17:43:01 GMT+0000 (Coordinated Universal Time)
cuid: clkpqc3ti000609l01rbu6dlc
slug: python-empowering-devops-with-automation-and-efficiency-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690738866598/2cef2765-5d4d-4e85-984b-82a26c3cd12d.png
tags: python3, devops-journey, 90daysofdevops, day14, trainwithshubham

---

---

# 📍Introduction

📚Welcome to Part 2 of the Python for DevOps Blog Series!🐍

In this blog, we will learn about the Non-primitive data types (aka Data structures). We will be learning Python from the basics to all the necessary things you will require for all your DevOps tasks. Let's unlock Python's potential in DevOps together!🌟

---

# 📍Lists

Lists is a mutable (i.e. can be changed) data structure that can store multiple values of any data type (including non-primitive) sequentially. It belongs to `<class 'list'>`. Lists can be initialized using `[]` brackets:

```python
list = [] # This is an empty list initialized
list = [1,2,4,"Varun","Margam",True,100.45]
print(type(list))

print(list) # To print the list.
```

Output:

```python
str = 'Varun'
list = list(str) # You can only put a sequential data type inside list()
print(list)
```

## ✔Accessing items in the List

Similar to how the characters in the string are positioned from 0 the items in the list are indexed from 0.

For example, `list = ['V','a','r','u','n']` is a list then `'V'` is stored in the index 0, `'a'` on the 1st index, `'r'` on the 2nd index, `'u'` on the 3rd index, and `'n'` on the 4th index. These items in the list can be accessed using these index positions:

```python
list = [1,2,4,"Varun","Margam",True,100.45]
      # 0,1,2,   3   ,   4    ,  5 ,  6  - index

print(list[0])
print(list[1])
print(list[2])
print(list[3])
print(list[4])
print(list[5])
print(list[6])

#We can also slice the list using the slicing operator [::] same as we saw in the string
#Example:
list[0::2]  #this will slice the list from the 0th index till the end but will skip 1 item in the list.
print(list)
#Run this code in your system and see the output for yourself.
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690722313971/d687cda8-609a-4eda-a167-9a0f0c0d9535.png align="center")

## ✔List Methods

There are many in-built List methods/functions provided by Python to be used for performing various operations on the list.

1. `.append(item)`: Appends the item at the end of the list.
    
2. `insert(index, item)`: Inserts the given item at the given index.
    
3. `.clear()`: Used to remove all the items in the string.
    
4. `.count(item)`: Counts the occurrence of the item mentioned.
    
5. `.extend(list_variable)`: Extends the list by adding all the items from the list\_variable at the end of the list.
    
6. `.reverse()`: Used to reverse the List.
    
7. `.sort()`: Sorts the list in ascending, descending, or by user-defined.
    
    and many more.
    
8. .`len()`: Returns the length of the list.
    

```python
list = [1,2,4,"Varun","Margam",True,100.45]

list.append(4)
print(list)
list.insert(2,3)  # Insert 3 at 2nd index
print(list)
list.count(4) # count the occurrence of 4 in the given list
print(list)
list.reverse()
print(list)

list2 = [9,5,6,8,10,7]

list2.sort()
print(list2)
list2.extend(list)
# It will add the elements of the list at the end of list2
print(list2)
list2.clear()
print(list2)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690723648914/63718ed1-cd22-4a2a-9cc2-27ecddef6431.png align="center")

---

# 📍Loops

Loops are used to execute a block of statements the desired number of times. In Python, we have 2 types of loops:

* For Loops
    
* While Loops
    

## ✔For Loops

Syntax:

```python
''' for iterator in sequence:  #This sequence can be anything that can be iterated.
      statements (you want to execute.) '''   

#Example
list = [1,2,4,"Varun","Margam",True,100.45]

for i in list:  # this i is an iterator that will iterate through every item in the list
    print(i)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690724431370/b7d40bdf-b7f8-4a7e-8d65-47572a311540.png align="center")

You can also iterate by indexes in range using for loops:

```python
list = [1,2,4,"Varun","Margam",True,100.45]

for index in range(0,5): # It will iterate from 0th index till 4th index
    print(list[index])
#Here, the index is an iterator that will iterate through the index of the items.
#in this range the concept of slicing can be applied like:
#range(0,len(list)) or range(0,6,2)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690724815767/29fab320-8a4f-44db-8870-1bea249172d4.png align="center")

We can also iterate through a string since it is also a sequence of characters:

```python
str = "Varun"

for char in str:
    print(char)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690725159197/9c2c3994-ca27-43b8-8017-ac5b05b8c015.png align="center")

## ✔While Loops

While loops are used when do not have any iterable sequence and we have to execute a block of code until the condition is satisfied.

```python
#Syntax
# while (condition):
#     statements
#     stopping condition
count = 0
while (count < 5):
    print(count)
    count += 1   # count = count + 1
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690726062332/09314afd-886a-4b5e-89ea-2a338d9ef0a7.png align="center")

Note: If we do not add the stopping statement in the body that dissatisfies the given condition then the condition will always be true and it will execute the statements forever making it an **Infinite While Loop**.

######## If I have time to explain the if-else block write about the break and pass statements as well.

---

# 📍Tuple

Tuples are data structures similar to Lists in Python, which store a sequence of values of any data type. Tuples are immutable (i.e. once a tuple is initialized then you cannot change the items inside the tuple). It belongs to `<class 'tuple'>`. Tuples are initialized using `()`:

```python
t = () # this is an empty tuple
t = (2,4,5,6,7,8)

print(t)
print(type(t))
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690727689441/05af9ccf-9891-4d62-96f1-fe42c4e4b4d0.png align="center")

```python
#Some Examples of tuple
t = 1,  # This is a tuple since denotes that it is a sequence.
print(type(t))
t = ("1") # This is not a tuple it is a string since it only contains 1 item.
print(type(t))
t = ("1",) # This is a tuple.
print(type(t))
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690727909115/e3560d23-f637-4cd4-82f7-60b643e7778b.png align="center")

You can access the items in the tuple using the index position. In Python, every sequence is indexed from 0. It is the same as we did in lists & strings.

```python
t = (2,4,5,6,7,8)

print(t[0])
print(t[5])

#We can also do tuple slicing same as we saw in lists and strings
print(t[::2])
print(t[1:4])

t[2] = 10  # This will throw an error since tuples are immutable
#You can execute the above line and see the error it displays
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690728366391/c0343f37-ef1d-4776-91f9-16605130e081.png align="center")

## ✔Unpacking in Tuple

I can assign individual items inside the tuple to a separate variable, this is called unpacking.

```python
t = (1,2,3) # It is a packed tuple
print(t)

a,b,c = (1,2,3)
print(a,b,c) # This is an unpacked tuple, 1,2,3 has been assigned to a,b, and c respectively.
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690729445717/2f487765-62e1-4559-8c4d-25f360e037c5.png align="center")

## ✔Tuple containing List

```python
t = ([1,2,3],2,3)

print(t)
print(t[0])
t[0].append(4)
print(t)
## Imp: Here, since t[0] is a list therefore we can make changes to it even if it is inside a tuple
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690730048966/e5dab62f-5e04-4a60-9a37-7abed146c2bd.png align="center")

## ✔List vs Tuple

* Tuples are immutable whereas Lists are mutable
    
* Tuples are much faster than Lists, since Tuple is fixed the memory allocated to the tuple in memory, is also fixed. For Lists as we can append items to the list memory is dynamically allocated making it slower.
    
* Tuples are declared using \[\] and Lists are declared using ().
    

---

# 📍Dictionary

A dictionary is a data structure that stores data sequentially in the form of `key: value` pair. The keys should be unique but the values can be repeated. It belongs to the `<class 'dict'>` in Python. It is initialized using `{}`.

```python
my_dict = {} # An empty dictionary has been initialized    
my_dict = {"name": "Varun", "Roll no": 31, "Gender": "Male"}
print(my_dict)
print(type(my_dict))
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690736768520/add9f7bf-f8ae-4c06-8db6-4c7b7e35e573.png align="center")

```python
my_dict = {"name": "Varun", "Roll no": 31, "Gender": "Male"}

print(my_dict["name"]) # It will give the keys corresponding value
my_dict["name"] = "Varun Margam" # You can change any key's value
print(my_dict)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690737212694/69d757a5-4715-4b1c-ac0e-9d3c6e668dfa.png align="center")

## ✔Dictionary Methods

* `.get("key")`: Returns the key's corresponding value. It has a Time complexity of O(1) i.e. very fast.
    
* `.keys()`: Returns the list of keys from the dictionary.
    
* `.values()`: Returns the list of values from the dictionary.
    
* `.items()`: Return the items i.e. the key, value pair of the dictionary.
    

```python
my_dict = {"name": "Varun", "Roll no": 31, "Gender": "Male"}

print(my_dict.get("Gender"))
print(my_dict.keys())
print(my_dict.values())
print(my_dict.items())
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690737580427/6e67635c-8936-4796-8bb2-f27ab0d86e8e.png align="center")

We can use these methods to iterate through the dictionary items, keys, or values.

```python
my_dict = {"name": "Varun", "Roll no": 31, "Gender": "Male"}

for key in my_dict.keys():  #the iterator key will iterate through all the keys
    print(key)

print("##############################")

for value in my_dict.values():
    print(value)

print("##############################")

for a,b in my_dict.items(): # a will iterate through all the keys and b through the values.
    print(a,b)   # or print(a,":",b)
```

Output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1690737983764/cdca1227-cadd-46e5-9be1-a4d01c7e2ecb.png align="center")

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, do share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [Python Playlist by TrainWithShubham](https://www.youtube.com/watch?v=bn-eH7BXyj4&list=PLlfy9GnSVerS_L5z0COaF7rsbgWmJXTOM&index=3)
    
* [GFG- List methods](https://www.geeksforgeeks.org/list-methods-in-python/)
    
* [Python playlist by CodeWithHarry](https://www.youtube.com/playlist?list=PLu0W_9lII9agwh1XjRt242xIpHhPT2llg)
    

---