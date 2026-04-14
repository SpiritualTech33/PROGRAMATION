We use this term, when we have delimiters symbols inside a parameter. It uses to wrap field where delimiter characters are used. 

**The quotechar tells the CSV parser:** _"Everything between these quotes is ONE field, ignore delimiters inside."_

python

```python
import csv

# Default quotechar (double quote)
with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f)  # quotechar='"' by default
    writer.writerow(['Yamil', 'Python, AI, ML', 'México'])
# Result: Yamil,"Python, AI, ML",México

# Custom quotechar (single quote)
with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quotechar="'")
    writer.writerow(['Yamil', 'Python, AI, ML', 'México'])
# Result: Yamil,'Python, AI, ML',México

# Custom quotechar (pipe - unusual but valid)
with open("file.csv", "w", newline='') as f:
    writer = csv.writer(f, quotechar="|")
    writer.writerow(['Yamil', 'Python, AI, ML', 'México'])
# Result: Yamil,|Python, AI, ML|,México
```
