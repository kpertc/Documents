#data #python 

[[Python File]]
[[Python OS, JSON]]

csv -> `,` delimited

``` python
import csv 

with open('file', 'r', newline='') as csv_file: 
	csv_reader = csv.reader(csv_file) 
	
	next(csv_reader) # skip the first line, usually header line 
	
	# write
	with open('new_csv', 'w', newline='') as new_file:
		csv_writer = csv.writer(new_file)
		
		for line in csv_reader: 
			print(line) # list of each line
			csv_writer.writerow(line)
```