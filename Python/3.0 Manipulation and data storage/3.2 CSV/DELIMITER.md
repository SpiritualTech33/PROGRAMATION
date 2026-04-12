The delimiter is the field separator between each individual data. By default, in csv files, the delimiter is the comma, but you can use different delimiters depending on the context. 

**Example with comma delimiter:**

```
nombre,edad,ciudad
Yamil,25,México
```

**Same data with semicolon delimiter:**

```
nombre;edad;ciudad
Yamil;25;México
```

**Same data with tab delimiter:**

```
nombre	edad	ciudad
Yamil	25	México
```

python

```python
import csv

# Default delimiter (comma)
with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f)  # delimiter=',' by default
    writer.writerow(['Yamil', '25', 'México'])
# Result: Yamil,25,México

# Custom delimiter (semicolon)
with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, delimiter=';')
    writer.writerow(['Yamil', '25', 'México'])
# Result: Yamil;25;México

# Tab delimiter (TSV - Tab Separated Values)
with open("file.tsv", "w", newline='') as f:
    writer = csv.writer(f, delimiter='\t')
    writer.writerow(['Yamil', '25', 'México'])
# Result: Yamil	25	México
```

### When to Use Different Delimiters

**Comma (`,`)** - Standard CSV

- Most common
- Universal compatibility

**Semicolon (`;`)** - European standard

- Used in countries where comma is decimal separator (e.g., `3,14` instead of `3.14`)
- Excel in Spanish/French/German uses `;` by default

**Tab (`\t`)** - TSV files

- When data contains many commas
- More visually clear in text editors

**Pipe (`|`)** - Database exports

- Less likely to appear in data
- Common in data warehousing