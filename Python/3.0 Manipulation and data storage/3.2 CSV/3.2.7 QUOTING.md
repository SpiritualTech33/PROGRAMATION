
## 4. QUOTING - The Quoting Strategy

### What It IS (Ontology)

**Quoting** determines **when to add quotes** around fields.

It's a **policy** - a rule for when to use the quotechar.

**Four strategies (constants in csv module):**

1. **`csv.QUOTE_MINIMAL`** (default) - Only quote when necessary
2. **`csv.QUOTE_ALL`** - Quote every field
3. **`csv.QUOTE_NONNUMERIC`** - Quote all non-numeric fields
4. **`csv.QUOTE_NONE`** - Never quote (dangerous!)


````python
import csv

with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_MINIMAL)
    writer.writerow(['Yamil', '25', 'México'])
    writer.writerow(['Carlos', 'Python, AI', 'España'])
```

**Result:**
```
Yamil,25,México
Carlos,"Python, AI",España
````

### 2. QUOTE_ALL

**Quote EVERY field, regardless:**



````python
import csv

with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_ALL)
    writer.writerow(['Yamil', '25', 'México'])
```

**Result:**
```
"Yamil","25","México"
````

### 3. QUOTE_NONNUMERIC

**Quote all fields EXCEPT pure numbers:**



````python
import csv

with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_NONNUMERIC)
    writer.writerow(['Yamil', 25, 'México'])  # 25 is int
```

**Result:**
```
"Yamil",25,"México"
````


### 4. QUOTE_NONE (Dangerous)

**Never quote anything:**

python

````python
import csv

with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quoting=csv.QUOTE_NONE, escapechar='\\')
    writer.writerow(['Yamil', 'Python, AI', 'México'])
```

**Result:**
```
Yamil,Python\, AI,México
        ↑ Escaped with backslash instead of quoted
````
