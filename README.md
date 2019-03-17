# SQL-EX.RU
### Exercise: 1 
Find the model number, speed and hard drive capacity for all the PCs with prices below $500.
```SQL
SELECT model, speed, hd
FROM PC
WHERE price < 500
```

### Exercise: 2
List all printer makers. 
```SQL
SELECT DISTINCT maker
FROM Product 
WHERE type = 'Printer'
```

### Exercise: 3
Find the model number, RAM and screen size of the laptops with prices over $1000.
```SQL
SELECT model, ram, screen
FROM Laptop
WHERE price > 1000
```

### Exercise: 4
Find all records from the Printer table containing data about color printers.
```SQL
SELECT *
FROM Printer
WHERE color = 'y'   
```

### Exercise: 5
Find the model number, speed and hard drive capacity of PCs cheaper than $600 having a 12x or a 24x CD drive.
```SQL
SELECT model, speed, hd
FROM PC 
WHERE price < 600 AND cd IN ('12X', '24X')
```