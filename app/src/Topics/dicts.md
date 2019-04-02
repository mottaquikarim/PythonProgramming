<!---
{"next": "Topics/loops.md","title": "Dicts"}
-->

# Dicts

In addition to lists, another more comprehensive method for storing complex data are **dicts**, or dictionaries. Dicts are key value pairs that act as another method for storing complex data.

## Basic Dict Concepts

```python
students = dict() # this creates a new, empty dict

# OR

tri-state_capitals = {
	'NY': 'Albany',
	'NJ': 'Trenton',
    'CT': 'Hartford'
}
```

In the example above, we associate a `key` - 'NY', 'NJ', 'CT' -  to a `value`, in this case the state's capital. Values can be any valid python datatype, but **keys must be strings.**

We can access each value in the list by referencing its key like so:

```python
print(tri-state_capitals['NJ']) # 'Trenton'
```

Attempting to find a key that does not exist leads to error:

```python
print(tri-state_capitals['PA']) # KeyError
```

Instead, better to use the `.get(key, [])` function like this:

```python
print(tri-state_capitals.get('PA', [])) # []
```

We can add this missing key to the dictionary like this:

```python
tri-state_capitals['PA'] = 'Philadelphia'
```

Here are two other examples of dicts, using lists and tuples as values for each key.

Lists as Values:

```python
students = {
  'taq': [86, 45, 98, 100],
  'sue': [100, 100, 100, 100],
  'jon': [38, 49, 90, 87],
}
```

Tuples as Values:

```python
wordFreqDic.update([ ('where', 4) , ('who', 5) , ('why', 6) , ('before' , 20)] )
```

## Sorting Dicts

Now, this dict has 4 keys, but what if it had hundreds? We can  retrieve keys, values, or items of dict in bulk as follows:

```python

student.keys() # ['taq', 'sue', 'jon', 'new_student']
student.values() # [[86, 45, 98, 100], [100, 100, 100, 100], etc ]
student.items() # [('taq', [86, 45, 98, 100]), ('sue', [100, 100, 100, 100]), etc]


dict = {'Name': 'Zabra', 'Age': 7}
print "Value : %s" %  dict.get('Age')
print "Value : %s" %  dict.get('Education', "Never")
When we run above program, it produces following result −

Value : 7
Value : Never
```

## Sorting Dicts




## 🚗 1. Simple Dict operations

1. Declare an empty dict
2. Create a dict containing the first and last names of 4 people.
3. Print the full name of the last person.
4. Add a 5th person to the dict index 2 of the dict.
5. Fill in the blanks of the following sentence:
"There are (blank) people in my dict. Their first names are ..."
6. Delete the person at index 2 from the dict.
5. Re-add the name you deleted to the end of the dict.

## 🚗 4. Sorting, Merging, & Slicing Dicts

1. Remember **[this](lists.md#-2-editing--manipulating-lists)** problem? You're still working on the playlist sort feature for Spotify, but now you have to take into account artist data for the songs. Using the expanded sample playlist below, alphabetize these songs.
Below is a list of titles from one user's playlist. Alphabetize these songs.
`playlist_titles = ["Rollin' Stone": ", "At Last', "Tiny Dancer", "Hey Jude", "Movin' Out"]`
2.