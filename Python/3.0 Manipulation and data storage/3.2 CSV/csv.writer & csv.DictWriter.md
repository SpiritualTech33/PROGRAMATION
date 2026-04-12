

## The Philosophy of Writing and Reading.

Before we code, understand this:
	**Reading CSV** = Receiving data (Yin - receptive)  
	**Writing CSV** = Creating/Manifesting data (Yang - active)


Okey, from the csv library, we can use 2 powerful tools to write in csv file. csv.writer and csv.DictWriter. They accomplish the same function, write text in csv with, but with subtle differences between them. 

# csv.writer
--- 
csv.writer, allow us to write in the csv file, row by row, respecting the base structure which you're writing. 

Basic usage and examples:

```python
import csv

with open("people.csv", mode="w", newline="", encoding="utf-8") as file:
    writer = csv.writer(file)

    writer.writerow(["id", "name", "age"])
    writer.writerow([1, "Carlos", 34])
    writer.writerow([2, "Rosa", 63])
    writer.writerow([3, "David", 29])

```

```python
#Writing individual rows
import csv

with open ("Training_log.csv" 'w' encoding='utf-8' newline='') as file:
	#Create the writer
	writer = csv.writer(file)
	
	#Write header (The line that shows the data structure)
	writer.writerow(['date', 'muscle trained' 'intensity'])
	
	#And write rows one by one
	writer.writerow(['23/02/2026', 'Chest', 'High'])
	writer.writerow(['24/02/2026', 'Back', 'Mid'])
	writer.writerow(['25/02/206', 'Legs', 'Very High'])
```

You can also write rows from structured data that was defined earlier.

```python
import csv

data = [ 

['nombre', 'edad', 'ciudad'], # Header row 
['Yamil', '25', 'México'], # Data row 1 
['Carlos', '30', 'España'], # Data row 2 
['Rosa', '28', 'Argentina'] # Data row 3

]

# Write to CSV 
with open("personas.csv", "w", encoding="utf8", newline='') as f: 
	writer = csv.writer(f)
	
	# Option 1: Write one row at a time 
	for row in data: w
		riter.writerow(row)
		
	
	# Option 2: Write all rows at once 
	 writer.writerows(data)

```

### Important: `newline=''`

Notice the `newline=''` parameter?

**Why it matters:**

- On Windows, without it, you get extra blank lines
- Python's `csv` module handles line endings internally
- **Always include `newline=''` when writing CSV**

it's very useful to write row by row. The only negative part, is that you have to remember the structure of the header, and cam be confusing sometimes, because it's not explicit. With that lack of explicitly on mind, we can move on into the other method. 


# csv.DictWriter
---
## The Professional Approach.

What this method does, is that write dictionary's in every single row, making more explicit and semantically clear, each row. 
This is **far more powerful** because you work with meaningful names, not list indices.

### Key concept: `fieldnames`

`fieldnames` is not a technical detail.  
It is a **contract with reality**.

Basic usage and examples:

```python
import csv

fieldnames = ["id", "name", "age"]

with open("people.csv", mode="w", newline="", encoding="utf-8") as file:
    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()

    writer.writerow({"id": 1, "name": "Carlos", "age": 34})
    writer.writerow({"id": 2, "name": "Rosa", "age": 63})
    writer.writerow({"id": 3, "name": "David", "age": 29})

```

```python
import csv

# Data as list of dictionaries

data = [
{'name':'Yamil', 'age': '25', 'city':'Yucatan'}
{'name':'Edgar', 'age':'27', 'city':'Florida'},
{'name':'Mariana', 'age':'32', 'city':'Ontario'}

]

with open ("personas.csv" 'w', encoding='utf-8', newlines='') as file:
	#Define the column named field names
	fieldnames = ['name', 'age', 'city]
	
	#Create the dictwriter
	writer = csv.DictWriter(file, fieldnames=fieldnames)
	
	#Write the header row (Column names)
	writer.writeheader()
	
	#Write all data in rows
	writer.writerows(data)
```

Writing row by row

```python
import csv

with open("meditation_log.csv", "w", encoding="utf8", newline='') as f:
    fieldnames = ['fecha', 'duracion', 'tecnica', 'estado']
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    
    writer.writeheader()
    
    # Write individual sessions
    writer.writerow({
        'fecha': '2026-02-03',
        'duracion': '30',
        'tecnica': 'Zazen',
        'estado': 'Calma profunda'
    })
    
    writer.writerow({
        'fecha': '2026-02-04',
        'duracion': '45',
        'tecnica': 'Vipassana',
        'estado': 'Insight sobre impermanencia'
    })
```

## **Important:** `fieldnames` defines the **column order** in the CSV:

```python
# This order
fieldnames = ['nombre', 'edad', 'ciudad']

# Produces this CSV
# nombre,edad,ciudad
# Yamil,25,México

# Different order
fieldnames = ['ciudad', 'nombre', 'edad']

# Produces different CSV
# ciudad,nombre,edad
# México,Yamil,25
```

Let's create something meaningful.

```python
import csv

# Your batting practice sessions (list of dicts - Exercise 5 pattern!)
sessions = [
    {
        'fecha': '2026-02-01',
        'swings': 100,
        'hits': 78,
        'home_runs': 5,
        'batting_avg': 0.780,
        'notas': 'Excelente timing hoy'
    },
    {
        'fecha': '2026-02-02',
        'swings': 100,
        'hits': 82,
        'home_runs': 7,
        'batting_avg': 0.820,
        'notas': 'Mejor sesión del mes'
    },
    {
        'fecha': '2026-02-03',
        'swings': 100,
        'hits': 75,
        'home_runs': 4,
        'batting_avg': 0.750,
        'notas': 'Cansancio afectó segunda mitad'
    }
]

# Write to CSV for analysis
with open("batting_stats.csv", "w", encoding="utf8", newline='') as f:
    fieldnames = ['fecha', 'swings', 'hits', 'home_runs', 'batting_avg', 'notas']
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    
    writer.writeheader()
    writer.writerows(sessions)

print("✅ Stats guardadas en batting_stats.csv")
```


# Best Practices:

✅ Always use `newline=''`
```python
with open("file.csv", "w", newline='') as f: # Good
```

✅ Always specify `encoding`
```python
with open("file.csv", "w", encoding="utf8", newline='') as f: # Good
```

✅ Prefer `DictWriter` for structured data
```python
# Better for maintainability
writer = csv.DictWriter(f, fieldnames=['nombre', 'edad'])
```

✅ Use meaningful fieldnames
```python
# Good 
fieldnames = ['player_name', 'batting_average', 'home_runs'] 
# Bad 
fieldnames = ['col1', 'col2', 'col3']
```
