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

### Exercise: 6
For each maker producing laptops with a hard drive capacity of 10 Gb or higher, find the speed of such laptops. Result set: maker, speed.
```SQL
SELECT DISTINCT maker, speed
FROM Product, Laptop
WHERE Product.model = Laptop.model AND hd >= 10
```

### Exercise: 7
Get the models and prices for all commercially available products (of any type) produced by maker B.
```SQL
SELECT Product.model, price
FROM Product, PC
WHERE maker = 'B'AND Product.model = PC.model
UNION
SELECT Product.model, price
FROM Product, Laptop
WHERE maker = 'B'AND Product.model = Laptop.model
UNION
SELECT Product.model, price
FROM Product, Printer
WHERE maker = 'B'AND Product.model = Printer.model
```

### Exercise: 8
Find the makers producing PCs but not laptops.
```SQL
SELECT DISTINCT maker 
FROM Product 
WHERE type = 'PC' AND 
 maker NOT IN (SELECT DISTINCT maker
               FROM Product
               WHERE type = 'Laptop')
```

### Exercise: 9
Find the makers of PCs with a processor speed of 450 MHz or more. Result set: maker.
```SQL
SELECT DISTINCT maker
FROM Product, PC
WHERE Product.model = PC.model 
 AND speed >= 450
```

### Exercise: 10
Find the printer models having the highest price. Result set: model, price.
```SQL
SELECT model, price
FROM Printer
WHERE price = (SELECT MAX(price)
               FROM printer)
```

### Exercise: 11
Find out the average speed of PCs.
```SQL
SELECT AVG(speed)
FROM PC
```

### Exercise: 12
Find out the average speed of the laptops priced over $1000.
```SQL
SELECT AVG(speed)
FROM Laptop
WHERE price > 1000
```

### Exercise: 13
Find out the average speed of the PCs produced by maker A.
```SQL
SELECT AVG(speed)
FROM Product,PC
WHERE Product.model = PC.model AND maker = 'A'
```

### Exercise: 14
Get the makers who produce only one product type and more than one model. Output: maker, type.  
方法一：
```SQL
SELECT maker, MAX/MIN(type) AS type
FROM Product
GROUP BY maker
HAVING COUNT(DISTINCT type) = 1 AND COUNT(model) > 1
```
方法二：
```SQL
SELECT DISTINCT maker, type
FROM Product
WHERE maker IN (SELECT maker
                FROM Product
                GROUP BY maker
                HAVING COUNT(DISTINCT type) = 1 
                       AND COUNT(model) > 1)
```