# db_any_company_global — Normalización de Base de Datos

## Descripción

Ejercicio de normalización de la tabla `sales_not_normalized` hasta tercera forma normal (3FN), aplicando claves primarias (PK) y foráneas (FK) para separar las entidades en tablas independientes, eliminando redundancia de datos.

---

## Tabla original — `sales_not_normalized`

```sql
CREATE TABLE sales_not_normalized (
    food_category    VARCHAR(100),
    food_subcategory VARCHAR(100),
    country          VARCHAR(50),
    country_code     CHAR(10),
    continent        VARCHAR(50),
    city             VARCHAR(50),
    unit_sales       BIGINT,
    date             DATE
);
```
## Diagrama de Chen

<img width="571" height="621" alt="Chen" src="https://github.com/user-attachments/assets/93a52f7c-acae-41b8-aef4-45dd2c3c4384" />

### Problemas detectados

- `continent` depende de `country`, no de la venta → redundancia
- `country_code` depende de `country`, no de la venta → redundancia
- `food_category` depende de `food_subcategory`, no de la venta → redundancia
- No existe clave primaria → no se puede identificar una fila de forma única


## Diagrama de base de datos normalizada — DBeaver

<img width="1709" height="790" alt="Diagrama" src="https://github.com/user-attachments/assets/2bbd7541-2743-45c1-9d24-65c332ee8395" />

---

## Script SQL final
```sql
SELECT co.country_name
FROM sales s
JOIN city ci      ON s.sales_id       = ci.city_id
JOIN country co   ON ci.country_id    = co.country_id
WHERE s.sales_id = 3;
```
**Output esperado:** `Canada`
---
<img width="1920" height="1022" alt="Canadá" src="https://github.com/user-attachments/assets/48397bf0-4435-459b-9a24-b691dba10633" />

## Tecnologías utilizadas

- SQLite
- DBeaver 26.1.1
- draw.io (diagrama de Chen)
---
