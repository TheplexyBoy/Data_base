# README SQL - Guía de Estudio (PostgreSQL)

## ¿Qué es SQL?
SQL es el lenguaje para consultar y administrar bases de datos.

## Orden de una consulta
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
7. LIMIT

## SELECT
```sql
SELECT * FROM clientes;
```

## WHERE
```sql
SELECT * FROM ventas WHERE cantidad>5;
```

## GROUP BY
Agrupa registros.
```sql
SELECT producto,SUM(cantidad)
FROM ventas
GROUP BY producto;
```

## HAVING
Filtra grupos.
```sql
SELECT producto,SUM(cantidad)
FROM ventas
GROUP BY producto
HAVING SUM(cantidad)>100;
```

## INNER JOIN
```sql
SELECT c.nombre,p.producto
FROM clientes c
INNER JOIN pedidos p
ON c.id=p.cliente_id;
```

## CRUD
INSERT, SELECT, UPDATE y DELETE.

## Consultas comunes
Producto más vendido:
```sql
SELECT p.product_name,SUM(f.quantity) total
FROM fact_sales f
INNER JOIN dim_product p ON f.product_id=p.product_id
GROUP BY p.product_name
ORDER BY total DESC;
```
