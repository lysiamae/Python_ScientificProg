# A structured array of whale species data
  ----
Turn the following data concerning various species of cetacean into a NumPy structured array and order it by (a) mass and (b) population. Determine in each case the index at which Bryde's whale (population: 100000, mass: 25 tonnes) should be inserted to keep the array ordered.

|Name|	Population|	Mass /tonnes|
|----|----|----|
|Bowhead whale|	9000|	60
|Blue whale	|20000|	120
|Fin whale|	100000|	70
|Humpback whale|	80000|	30
|Gray whale|	26000|	35
|Atlantic white-sided dolphin|	250000|	0.235
|Pacific white-sided dolphin|	1000000|	0.15
|Killer whale|	100000|	4.5
|Narwhal|	25000|	1.5
|Beluga	|100000	|1.5
|Sperm whale|	2000000	|50
|Baiji|	13|	0.13
|North Atlantic right whale|	300|	75
|North Pacific right whale	|200|	80
|Southern right whale|	7000|	70


A text file containing these data is available as [whale-data.txt](https://scipython.com/static/media/2/problems/P6.1/whale-data.txt)



My solution is shown below. I have used Google Colab to execute the following python code.
### SOLUTION: 
```python
import numpy as np  #imports the numpy lib package

#set the type for each variable
dt = np.dtype([('Common Name', 'S32'),('Population','i4'),('Mass','f8')])

#populate a structured array in the arbitrary order given, Insert the date type
cetaceans = np.array([('Bowhead whale',9000,60),('Blue whale', 20000,120),('Fin whale',	100000,	70), ('Humpback whale',	80000,	30), ('Gray whale',	26000,	35),('Atlantic white-sided dolphin',	250000,	0.235),
('Pacific white-sided dolphin',	1000000,	0.15),('Killer whale',	100000,	4.5),('Narwhal',	25000,	1.5),('Beluga',	100000,	1.5),('Sperm whale',	2000000,	50),
('Baiji',	13,	0.13),('North Atlantic right whale',	300,	75),
('North Pacific right whale',	200,	80),
('Southern right whale'	,7000,	70)], dtype= dt)

#Sorting by mass
cetaceans.sort(order='Mass')

#Insert the new whale and find by the index where to insert it
new_whale = np.array(("Bryde's whale", 100000, 25), dtype=dt)
np.searchsorted(cetaceans['Mass'], new_whale['Mass'])

# order by population and find again where to insert new whale
cetaceans.sort(order="Population")
np.searchsorted(cetaceans['Population'], new_whale['Population'])
```



