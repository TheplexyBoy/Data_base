# Consultas SQL - Casos de Uso

## 1. Administrador de Operaciones

### Objetivo
Consultar cuáles bodegas presentan mayor actividad dentro de la organización.

### Consulta

```sql
SELECT TOP 10
    b.nombre_bodega,
    COUNT(*) AS total_actividades
FROM HechosVentas hv
JOIN DimBodega b
    ON hv.id_bodega = b.id_bodega
GROUP BY b.nombre_bodega
ORDER BY total_actividades DESC;
```

### Explicación

- `JOIN` une la tabla de hechos con la dimensión de bodegas.
- `COUNT(*)` cuenta cuántas operaciones realizó cada bodega.
- `GROUP BY` agrupa los registros por bodega.
- `ORDER BY DESC` ordena de mayor a menor actividad.
- `TOP 10` muestra únicamente las diez bodegas con mayor actividad.

---

## Top 10 clientes que más compran

### Consulta

```sql
SELECT TOP 10
    c.nombre_cliente,
    SUM(hv.cantidad) AS total_comprado
FROM HechosVentas hv
JOIN DimCliente c
    ON hv.id_cliente = c.id_cliente
GROUP BY c.nombre_cliente
ORDER BY total_comprado DESC;
```

### Explicación

Esta consulta permite identificar los clientes con mayor cantidad de productos comprados.

---

## 2. Analista

### Objetivo

Identificar el producto con mayor rotación dentro de la organización.

### Consulta

```sql
SELECT TOP 1
    p.nombre_producto,
    SUM(hv.cantidad) AS unidades_vendidas
FROM HechosVentas hv
JOIN DimProducto p
    ON hv.id_producto = p.id_producto
GROUP BY p.nombre_producto
ORDER BY unidades_vendidas DESC;
```

### Explicación

- Se agrupan las ventas por producto.
- Se suman todas las unidades vendidas.
- Se ordenan de mayor a menor.
- `TOP 1` devuelve el producto más vendido.

---

## Top 10 productos más vendidos

```sql
SELECT TOP 10
    p.nombre_producto,
    SUM(hv.cantidad) AS unidades_vendidas
FROM HechosVentas hv
JOIN DimProducto p
    ON hv.id_producto = p.id_producto
GROUP BY p.nombre_producto
ORDER BY unidades_vendidas DESC;
```

---

## 3. Gerente de Operaciones

### Objetivo

Conocer el valor económico del inventario distribuido en cada bodega.

### Consulta

```sql
SELECT
    b.nombre_bodega,
    SUM(i.stock * p.costo_unitario) AS valor_inventario
FROM Inventario i
JOIN DimBodega b
    ON i.id_bodega = b.id_bodega
JOIN DimProducto p
    ON i.id_producto = p.id_producto
GROUP BY b.nombre_bodega
ORDER BY valor_inventario DESC;
```

### Explicación

- Se relacionan las tablas de inventario, productos y bodegas.
- El valor del inventario se obtiene multiplicando el stock por el costo unitario.
- Se agrupa el resultado por bodega.
- Finalmente se ordena de mayor a menor valor económico.

---

# Funciones SQL utilizadas

| Función | Descripción |
|----------|-------------|
| `SELECT` | Selecciona las columnas que se desean consultar. |
| `FROM` | Indica la tabla principal de donde se obtendrán los datos. |
| `JOIN` | Relaciona dos o más tablas mediante una llave. |
| `ON` | Especifica la condición de la relación entre tablas. |
| `GROUP BY` | Agrupa los registros según una columna. |
| `COUNT()` | Cuenta la cantidad de registros por grupo. |
| `SUM()` | Suma valores numéricos de una columna. |
| `ORDER BY` | Ordena los resultados. |
| `DESC` | Orden descendente (de mayor a menor). |
| `TOP` | Limita el número de registros devueltos. |

---

# Resumen

| Rol | Información requerida | Función principal |
|------|------------------------|-------------------|
| Administrador de Operaciones | Bodegas con mayor actividad | `COUNT()` |
| Administrador de Operaciones | Top 10 clientes que más compran | `SUM()` |
| Analista | Producto con mayor rotación | `SUM()` |
| Gerente de Operaciones | Valor económico del inventario por bodega | `SUM(stock × costo)` |
