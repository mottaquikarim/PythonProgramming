<!---
{"next":"About/README.md","title":"Tips & Tricks"}
-->

# Tips & Tricks

## Why a += b isn't always the same as a = a + b in Python
*Source: [https://www.geeksforgeeks.org/python-a-b-is-not-always-a-a-b/](https://www.geeksforgeeks.org/python-a-b-is-not-always-a-a-b/)*

#### Example 1
```python
list1 = [5, 4, 3, 2, 1] 
list2 = list1 
list1 += [1, 2, 3, 4] 

print(list1) # [5, 4, 3, 2, 1, 1, 2, 3, 4]
print(list2) # [5, 4, 3, 2, 1, 1, 2, 3, 4]
```

#### Example 2
```python
list1 = [5, 4, 3, 2, 1] 
list2 = list1 
list1 = list1 + [1, 2, 3, 4] 

print(list1) # [5, 4, 3, 2, 1, 1, 2, 3, 4]
print(list2) # [5, 4, 3, 2, 1]
```

In Example 2, the contents of list1 are the same as in Example 1, but the contents of list2 are different. 

* expression list1 += [1, 2, 3, 4] changes the existing declaration of list1. Because list2 is pointing at list1, list2 now references the extended list of numbers in list1.

* expression list1 = list1 + [1, 2, 3, 4] re-declares list1, assigning it a new, longer list of numbers. In doing so, it creates a new list and changes “list1” reference to that new list, while and “list2” still points to the original declaration of list1.
