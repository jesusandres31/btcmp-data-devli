# Semana 4 · Clase 8

## 💬 1. Repaso + conexión a la DB

Crear la tabla:

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary NUMERIC,
    hire_date DATE
);
```

Insertar algunos registros:

```sql
INSERT INTO employees (name, department, salary, hire_date) VALUES
('Ana', 'IT', 5000, '2021-03-15'),
('Carlos', 'HR', 4200, '2022-06-10'),
('Laura', 'IT', 5600, '2020-11-05'),
('Mateo', 'Finance', 4800, '2023-01-12'),
('Lucía', 'Finance', 4700, '2022-09-25'),
('Sofía', 'Marketing', 4500, '2021-08-03'),
('Diego', 'IT', 6000, '2019-12-17'),
('Valentina', 'HR', 4300, '2023-04-22'),
('Andrés', 'Finance', 5100, '2020-05-09'),
('Camila', 'Marketing', 4600, '2022-02-28'),
('Marcos', 'IT', 5500, '2021-07-19'),
('Isabella', 'HR', 4400, '2020-10-12'),
('Juliana', 'Finance', 4950, '2023-03-08'),
('Nicolás', 'Marketing', 4700, '2021-12-15'),
('Fernanda', 'IT', 5800, '2022-05-30');
```

## 🧠 2. Primeras consultas SQL

Estructura general:

```sql
SELECT columnas
FROM tabla
[WHERE condición]
[ORDER BY columna]
[LIMIT número];
```

Ejemplos básicos:

```sql
-- Ver toda la tabla
SELECT * FROM employees;

-- Ver solo nombre y salario
SELECT name, salary FROM employees;

-- Cambiar el alias de columna
SELECT name AS "Empleado", salary AS "Sueldo" FROM employees;

-- Cambiar el salario de un empleado específico
UPDATE employees
SET salary = 6000
WHERE name = 'Laura';

-- Eliminar una tabla temporal de ejemplo
DROP TABLE IF EXISTS temp_table;

-- Eliminar un empleado específico
DELETE FROM employees
WHERE id = 3;  -- Por ejemplo, Laura

-- Eliminar todos los registros de la tabla (¡peligroso!)
DELETE FROM employees;
```

## ⚙️ 3. Filtros y operadores

Operadores básicos de `WHERE`:

- Comparación: `=`, `>`, `<`, `>=`, `<=`, `!=`
- Lógicos: `AND`, `OR`, `NOT`
- Otros: `IN`, `BETWEEN`, `LIKE`

Ejemplos:

```sql
-- Empleados del área IT
SELECT * FROM employees WHERE department = 'IT';

-- Salario mayor a 4800
SELECT * FROM employees WHERE salary > 4800;

-- Empleados contratados después de 2022
SELECT * FROM employees WHERE hire_date > '2022-01-01';

-- Empleados con salario entre 4500 y 5500
SELECT * FROM employees WHERE salary BETWEEN 4500 AND 5500;

-- Nombre empieza con 'L'
SELECT * FROM employees WHERE name LIKE 'L%';
```

## 📊 4. Funciones agregadas y agrupamientos

- `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`
- `GROUP BY` y `HAVING`

Ejemplos:

```sql
-- Cuántos empleados hay
SELECT COUNT(*) FROM employees;

-- Promedio salarial
SELECT AVG(salary) FROM employees;

-- Salario máximo por departamento
SELECT department, MAX(salary)
FROM employees
GROUP BY department;

-- Departamentos con salario promedio > 4500
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 4500;
```

## 🧩 5. Mini desafío

Crear la tabla:

```sql
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    product VARCHAR(50),
    category VARCHAR(30),
    price NUMERIC,
    quantity INT,
    sale_date DATE
);
```

Insertar los datos:

```sql
INSERT INTO sales (product, category, price, quantity, sale_date) VALUES
('Mouse', 'Electronics', 15, 4, '2023-07-10'),
('Keyboard', 'Electronics', 30, 2, '2023-07-11'),
('Notebook', 'Stationery', 8, 10, '2023-07-12'),
('Pen', 'Stationery', 2, 25, '2023-07-13'),
('Headphones', 'Electronics', 40, 3, '2023-07-14'),
('Monitor', 'Electronics', 120, 1, '2023-07-15'),
('Desk Chair', 'Furniture', 85, 2, '2023-07-16'),
('Notebook Case', 'Accessories', 25, 3, '2023-07-17'),
('Printer Paper', 'Stationery', 6, 15, '2023-07-18'),
('USB Drive', 'Electronics', 12, 5, '2023-07-19'),
('Desk Lamp', 'Furniture', 35, 4, '2023-07-20'),
('Stapler', 'Stationery', 7, 6, '2023-07-21'),
('Calculator', 'Electronics', 20, 3, '2023-07-22'),
('Water Bottle', 'Accessories', 10, 8, '2023-07-23'),
('Laptop Stand', 'Accessories', 45, 2, '2023-07-24'),
('Office Desk', 'Furniture', 150, 1, '2023-07-25'),
('Whiteboard', 'Furniture', 60, 1, '2023-07-26'),
('Marker Set', 'Stationery', 5, 12, '2023-07-27'),
('Mouse Pad', 'Accessories', 8, 7, '2023-07-28'),
('Webcam', 'Electronics', 50, 2, '2023-07-29'),
('Smartphone', 'Electronics', 300, 1, '2023-07-30'),
('Notebook Pro', 'Electronics', 900, 1, '2023-07-31'),
('File Cabinet', 'Furniture', 120, 1, '2023-08-01'),
('Backpack', 'Accessories', 40, 3, '2023-08-02'),
('Binder', 'Stationery', 4, 20, '2023-08-03'),
('Headset Stand', 'Accessories', 15, 5, '2023-08-04'),
('Desk Organizer', 'Accessories', 12, 6, '2023-08-05'),
('Laptop Sleeve', 'Accessories', 30, 2, '2023-08-06'),
('Paper Clips', 'Stationery', 1, 50, '2023-08-07'),
('Surge Protector', 'Electronics', 25, 3, '2023-08-08'),
('Pen Holder', 'Accessories', 5, 10, '2023-08-09');
```

### Ejercicios

1. Mostrar todas las ventas de la categoría "Electronics".
2. Calcular el total de ingresos por categoría (`price * quantity`).
3. Obtener la categoría con mayor ingreso total.
4. Mostrar todas las ventas donde el precio del producto sea mayor a 20.
5. Calcular el total de unidades vendidas (`SUM(quantity)`) por cada producto.
6. Calcular el ingreso promedio por venta (`AVG(price * quantity)`) para cada producto.
7. Mostrar los 3 productos con mayor cantidad total vendida (`SUM(quantity)`) usando `ORDER BY` y `LIMIT`.
8. Mostrar todas las ventas realizadas después del 12 de julio de 2023.
9. Mostrar la categoría y el ingreso total, pero solo para categorías cuyo ingreso sea mayor a 50 (`HAVING SUM(price * quantity) > 50`).
10. Mostrar todas las ventas donde el nombre del producto comience con la letra H (`LIKE 'H%'`).
11. Calcular la cantidad promedio de productos vendidos (`AVG(quantity)`) agrupados por categoría.
12. Mostrar todas las ventas y calcular el ingreso por fila (`price * quantity`), ordenadas de mayor a menor ingreso.
13. Mostrar todas las ventas de la categoría `'Electronics'` donde la cantidad sea mayor a 2 y el precio menor a 40.
