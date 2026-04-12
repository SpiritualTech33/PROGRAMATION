

## The Philosophy of Writing and Reading.

Before we code, understand this:
	**Reading CSV** = Receiving data (Yin - receptive)  
	**Writing CSV** = Creating/Manifesting data (Yang - active)

Well, in the last note we talk about the csv.writer and DictWriter methods. And, how his name suggests, those are tools that let us write in csv files. Now, we're gonna see the oposite; How to read them.

A CSV file is silent ink.  
`csv.reader` and `csv.DictReader` are the **acts of understanding**.

They do not change the file.  
They change **how the file appears to your mind**.

Let's begin with csv.reader, the most simple of both. what it does? simple, reads the text by rows. Returns a list foe each row. Simple, direct, index-based access.

Basic Example

```python
import csv

with open("people.csv", mode="r", encoding="utf-8") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)

#Output
['id', 'name', 'age']
['1', 'Carlos', '34']
['2', 'Rosa', '63']
['3', 'David', '29']
```

Note somethin crucial. Everything is a string, no types, no meaning, just structure. 
In this case index [0] is not 'id' is just the first thing. 

Skipping the header
```python
import csv

with open ("Personas.csv", 'r', encoding='utf-8') as file:
	reader = csv.reader(file)
	#Skip the header row
	next(reader) #Moves past the first row
	
	for row in reader:
		id_number = row[0]
		name = row[1]
		age = row[2]
		print(f"{name} has {age} years old, and lives in {city})
```






Now, let's move into csv.DictReader
### Metaphysical posture

`csv.DictReader` believes:

> Meaning should be bound to value.

It uses the **header row** as a schema.

This is interpretation grounded in declared form.

Basic example

```python
import csv

with open ("Pruebas.csv", 'r', encoding='utf-8') as file:
	reader = csv.DictReader(file)
	for row in reader:
		print(row)
		
#Output
{'id': '1', 'name': 'Carlos', 'age': '34'}
{'id': '2', 'name': 'Rosa', 'age': '63'}
{'id': '3', 'name': 'David', 'age': '29'}

```

Each row will be a dictionary. Now, every position is not only a number, has identity and meaning. 

You can access data by name:
```python
import csv

with open ("example.csv", 'r', encoding='utf-8') as file:
	reader = csv.DictReader(file)
	
	for row in reader:
	#Acces by keyname (clear, semantic)
		id_number = row['id']
		name = row['name']
		age = row['age']
		print(f"{id_number} ({name}) has {age} years old")
```

compare to csv.reader
```python
# csv.reader - index-based (what's 0? 1? 2?) 
id_number = row[0] 
name = row[1] 
age = row[2] 

# csv.DictReader - name-based (clear, explicit) 
id_number = row['id'] 
name = row['name'] 
age = row['age']
```

DictReader = Self-documenting code.

##  Comparison: reader vs DictReader

|Feature|`csv.reader`|`csv.DictReader`|
|---|---|---|
|**Returns**|Lists|Dictionaries|
|**Access**|By index: `row[0]`|By name: `row['nombre']`|
|**Header**|Manual handling|Automatic|
|**Clarity**|Less|**Much more**|
|**Flexibility**|Basic|Advanced|
|**Use When**|Simple parsing|**Professional work**|

## ⚖️ `reader` vs `DictReader`

| Dimension  | csv.reader          | csv.DictReader    |
| ---------- | ------------------- | ----------------- |
| Structure  | Lists               | Dictionaries      |
| Meaning    | Implicit            | Explicit          |
| Schema     | Mental              | Declared (header) |
| Risk       | Silent misalignment | Key errors        |
| Clarity    | Low                 | High              |
| Philosophy | Empiricism          | Hermeneutics      |




# 7. Best Practices


### ✅ Prefer `DictReader` for structured data

python

```python
# Clear, maintainable, professional
reader = csv.DictReader(f)
for row in reader:
    print(row['nombre'])
```

### ✅ Convert to list when needed

python

```python
# For multiple passes or indexing
data = list(csv.DictReader(f))
```

### ✅ Always specify encoding

python

```python
with open("file.csv", "r", encoding="utf8") as f:
```

### ✅ Handle custom delimiters

python

```python
reader = csv.DictReader(f, delimiter=';')
```