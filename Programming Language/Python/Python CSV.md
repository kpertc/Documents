#data 

[[Python File]]
[[Python OS, JSON]]

csv -> `,` delimited

``` python
import csv 

with open('file', 'r') as csv_file: 
	csv_reader = csv.reader(csv_file) 
	
	next(csv_reader) # skip the first line, usually header line 
	
	for line in csv_reader: 
		print(line) # list of each line with open('new_csv', 'w') as new file
```