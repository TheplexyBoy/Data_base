# 📚 README SQL - Chuleta Completa PostgreSQL

> Guía rápida de SQL para PostgreSQL.

# SELECT

## Sintaxis

```sql
SELECT columna1, columna2
FROM tabla;
```

### ¿Qué hace?
Selecciona las columnas que quieres mostrar.

### Ejemplo

```sql
SELECT nombre, ciudad
FROM clientes;
```

---

# SELECT *

```sql
SELECT *
FROM productos;
```

Trae todas las columnas.

---

# DISTINCT

```sql
SELECT DISTINCT ciudad
FROM clientes;
```

Elimina registros repetidos.

---

# WHERE

```sql
SELECT *
FROM ventas
WHERE cantidad > 5;
```

Filtra filas.

---

# Operadores

- `=`
- `<>`
- `>`
- `<`
- `>=`
- `<=`

Ejemplo:

```sql
SELECT *
FROM empleados
WHERE salario >= 2500;
```

---

# AND

```sql
SELECT *
FROM clientes
WHERE ciudad='Barranquilla'
AND edad>18;
```

Todas las condiciones deben cumplirse.

---

# OR

```sql
SELECT *
FROM clientes
WHERE ciudad='Barranquilla'
OR ciudad='Bogotá';
```

Con que una condición sea verdadera, el registro aparece.

---

# NOT

```sql
SELECT *
FROM clientes
WHERE NOT ciudad='Barranquilla';
```

Niega una condición.

---

# ORDER BY

```sql
SELECT *
FROM productos
ORDER BY precio DESC;
```

Ordena los resultados.

- `ASC`: Ascendente.
- `DESC`: Descendente.

---

# LIMIT

```sql
SELECT *
FROM productos
LIMIT 10;
```

Limita la cantidad de filas.

---

# OFFSET

```sql
SELECT *
FROM productos
LIMIT 10 OFFSET 20;
```

Omite registros antes de mostrar resultados.

---

# LIKE

```sql
LIKE 'A%'
LIKE '%ez'
LIKE '%an%'
```

Ejemplo:

```sql
SELECT *
FROM clientes
WHERE nombre LIKE 'A%';
```

---

# IN

```sql
SELECT *
FROM clientes
WHERE ciudad IN ('Barranquilla','Bogotá');
```

Busca varios valores.

---

# BETWEEN

```sql
SELECT *
FROM ventas
WHERE precio BETWEEN 1000 AND 5000;
```

Busca dentro de un rango.

---

# IS NULL

```sql
SELECT *
FROM clientes
WHERE telefono IS NULL;
```

Busca valores vacíos.

---

# COUNT

```sql
SELECT COUNT(*)
FROM ventas;
```

Cuenta registros.

---

# SUM

```sql
SELECT SUM(precio)
FROM ventas;
```

Suma valores.

---

# AVG

```sql
SELECT AVG(precio)
FROM ventas;
```

Calcula el promedio.

---

# MAX

```sql
SELECT MAX(precio)
FROM ventas;
```

Obtiene el mayor valor.

---

# MIN

```sql
SELECT MIN(precio)
FROM ventas;
```

Obtiene el menor valor.

---

# ROUND

```sql
SELECT ROUND(AVG(precio),2)
FROM ventas;
```

Redondea decimales.

---

# GROUP BY

```sql
SELECT producto, SUM(cantidad)
FROM ventas
GROUP BY producto;
```

Agrupa registros para hacer cálculos.

---

# HAVING

```sql
SELECT producto, SUM(cantidad)
FROM ventas
GROUP BY producto
HAVING SUM(cantidad)>100;
```

Filtra grupos.

> **WHERE** filtra filas.  
> **HAVING** filtra grupos.

---

# AS

```sql
SELECT nombre AS Cliente
FROM clientes;
```

Cambia el nombre de una columna temporalmente.

---

# INNER JOIN

```sql
SELECT c.nombre, p.producto
FROM clientes c
INNER JOIN pedidos p
ON c.id=p.cliente_id;
```

Solo devuelve coincidencias.

---

# LEFT JOIN

```sql
SELECT *
FROM clientes
LEFT JOIN ventas
ON clientes.id=ventas.cliente_id;
```

Devuelve todos los registros de la tabla izquierda.

---

# RIGHT JOIN

```sql
SELECT *
FROM clientes
RIGHT JOIN ventas
ON clientes.id=ventas.cliente_id;
```

Devuelve todos los registros de la derecha.

---

# FULL JOIN

```sql
SELECT *
FROM clientes
FULL JOIN ventas
ON clientes.id=ventas.cliente_id;
```

Devuelve todos los registros de ambas tablas.

---

# CROSS JOIN

```sql
SELECT *
FROM clientes
CROSS JOIN productos;
```

Genera todas las combinaciones posibles.

---

# CREATE DATABASE

```sql
CREATE DATABASE tienda;
```

Crea una base de datos.

---

# CREATE TABLE

```sql
CREATE TABLE clientes(
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(100),
    edad INT
);
```

Crea una tabla.

---

# Tipos de datos

- INT
- BIGINT
- SMALLINT
- NUMERIC
- DECIMAL
- FLOAT
- VARCHAR
- CHAR
- TEXT
- BOOLEAN
- DATE
- TIME
- TIMESTAMP

---

# PRIMARY KEY

```sql
id SERIAL PRIMARY KEY;
```

Identifica un registro de forma única.

---

# FOREIGN KEY

```sql
FOREIGN KEY(cliente_id)
REFERENCES clientes(id);
```

Relaciona tablas.

---

# INSERT

```sql
INSERT INTO clientes(nombre,edad)
VALUES ('Andres',19);
```

Inserta datos.

---

# UPDATE

```sql
UPDATE clientes
SET edad=20
WHERE id=1;
```

Actualiza datos.

---

# DELETE

```sql
DELETE FROM clientes
WHERE id=1;
```

Elimina registros.

---

# TRUNCATE

```sql
TRUNCATE TABLE clientes;
```

Elimina todos los registros de una tabla.

---

# DROP TABLE

```sql
DROP TABLE clientes;
```

Elimina completamente la tabla.

---

# ALTER TABLE

Agregar columna:

```sql
ALTER TABLE clientes
ADD telefono VARCHAR(20);
```

Eliminar columna:

```sql
ALTER TABLE clientes
DROP COLUMN telefono;
```

Modificar tipo:

```sql
ALTER TABLE clientes
ALTER COLUMN edad TYPE BIGINT;
```

---

# CASE

```sql
SELECT nombre,
CASE
WHEN edad>=18 THEN 'Mayor'
ELSE 'Menor'
END AS categoria
FROM clientes;
```

Funciona como un `IF`.

---

# COALESCE

```sql
SELECT COALESCE(telefono,'Sin teléfono')
FROM clientes;
```

Reemplaza valores `NULL`.

---

# Subconsulta

```sql
SELECT *
FROM productos
WHERE precio >
(
SELECT AVG(precio)
FROM productos
);
```

Una consulta dentro de otra.

---

# VIEW

```sql
CREATE VIEW ventas2026 AS
SELECT *
FROM ventas
WHERE anio=2026;
```

Guarda una consulta como una vista.

---

# INDEX

```sql
CREATE INDEX idx_nombre
ON clientes(nombre);
```

Acelera las búsquedas.

---

# Orden de ejecución de SQL

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
7. LIMIT

---

# Consulta completa

```sql
SELECT c.customer_name,
SUM(f.quantity*f.unit_price) AS total

FROM fact_sales f

INNER JOIN dim_customer c
ON f.customer_id=c.customer_id

WHERE f.activity='Sale'

GROUP BY c.customer_name

HAVING SUM(f.quantity)>50

ORDER BY total DESC

LIMIT 10;
```
