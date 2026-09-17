## Pregunta 1 - Catálogo comercial activo

**Enunciado:** Obtén los productos que no están descatalogados y cuyo precio unitario esté entre 10 y 50 euros, ambos incluidos. Muestra el nombre del producto y su precio redondeado a dos decimales, ordenado de mayor a menor precio.

**Consulta:**

```sql
SELECT product_name, ROUND(unit_price::numeric, 2)
FROM products
WHERE discontinued = 0 AND unit_price::numeric BETWEEN 10 AND 50
ORDER BY unit_price::numeric DESC;
```

**Resultado:**



**Comentario:** He usado WHERE para filtrar que el precio este entre 2 parámetros y los productos que no estén descatalogados, y he usado el ORDER BY DESC para ordenar de mayor a menor.

---

## Pregunta 2 - Concentración geográfica de la cartera

**Enunciado:** Cuenta cuántos clientes hay en cada país y muestra únicamente aquellos países con 5 o más clientes, ordenados de mayor a menor. Indica también cuántas ciudades distintas hay en cada uno de esos países.

**Consulta:**

```sql
SELECT 
    country AS pais, 
    COUNT(customer_id) AS num_clientes, 
    COUNT(DISTINCT city) AS num_ciudades
FROM 
    customers
GROUP BY 
    country
HAVING 
    COUNT(customer_id) >= 5
ORDER BY 
    num_clientes DESC;
```

**Resultado:**



**Comentario:** 

---

## Pregunta 3 — Alerta de reposición

**Enunciado:** Localiza los productos activos cuyas unidades en stock sean inferiores o iguales a su nivel de reposición. Muestra el nombre, las unidades en stock, el nivel de reposición, las unidades ya pedidas al proveedor y una columna de texto que indique 'CRÍTICO' cuando el stock sea 0 y 'AVISO' en el resto de casos.

**Consulta:**

```sql
SELECT 
    product_name AS producto, 
    units_in_stock AS stock, 
    reorder_level AS nivel_reposicion, 
    units_on_order AS pedido_a_proveedor,
    CASE 
        WHEN units_in_stock = 0 THEN 'CRÍTICO'
        ELSE 'AVISO'
    END AS situacion
FROM 
    products
WHERE 
    discontinued = 0 
    AND units_in_stock <= reorder_level;
```

**Resultado:**



**Comentario:** 

--- 

## Pregunta 4 - Ficha completa de producto

**Enunciado:** Para los productos suministrados por empresas de Italia, Francia o España, muestra el nombre del producto, el nombre de la categoría, el nombre del proveedor, su país y su ciudad. Ordena por país y, dentro de cada país, por nombre de producto.

**Consulta:**

```sql
SELECT p.product_name AS producto,
	c.category_name AS categoria,
	s.company_name AS proveedor,
	s.country AS pais,
	s.city AS ciudad
FROM 
	products p
INNER JOIN suppliers s ON p.supplier_id = s.supplier_id
INNER JOIN categories c ON p.category_id = c.category_id
WHERE s.country IN('Italy', 'Spain', 'French')
ORDER BY s.country ASC, 
p.product_name ASC;

```

**Resultado:**



**Comentario:** 

---

## Pregunta 5 - Detalle valorizado de un pedido

**Enunciado:** Atención al cliente recibe una reclamación sobre el pedido **10248** y necesita reconstruir la factura línea a línea.

Muestra, para ese pedido, el nombre del producto, el precio unitario aplicado, la cantidad, el descuento y el importe final de cada línea. Añade el nombre del cliente y la fecha del pedido.

**Consulta:**

```sql
SELECT contact_name AS cliente,
	o.order_date AS fecha_pedido,
	p.product_name AS producto,
	p.unit_price AS precio_unitario,
	d.quantity AS cantidad,
	d.discount AS descuento,
	ROUND((p.unit_price::numeric) * d.quantity * (1 - d.discount::numeric), 2) AS importe_linea
FROM 
	order_details AS d
INNER JOIN orders AS o USING(order_id)
INNER JOIN products AS p USING(product_id)
INNER JOIN customers AS c ON c.customer_id = o.customer_id
WHERE o.order_id = 10248
```

**Resultado:**



**Comentario:** 

---

## Pregunta 6

**Enunciado:** Comité de dirección: ¿qué familias de producto sostienen realmente el negocio?

Calcula la facturación total de cada categoría durante toda la historia de la compañía. Muestra el nombre de la categoría, el número de líneas de pedido que ha generado, el número de productos distintos vendidos y la facturación total. Incluye únicamente las categorías que superen los **100.000 euros** de facturación, ordenadas de mayor a menor.

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 7

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 8

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 9

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 10

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 11

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 12

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---

## Pregunta 13

**Enunciado:** 

**Consulta:**

```sql

```

**Resultado:**



**Comentario:** 

---
