---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Ejercicios

## Ejercicio 1

Mostrar las columnas `NOMBRE`, `APELLIDO1`, `EDAD` y `DNI` de la tabla `PERSONAS` ordenadas por el `DNI` de menor a mayor y cuya edad sea superior a 40 años.

````{admonition} Solución
:class: dropdown
```sql
SELECT nombre, apellido1, edad, dni FROM personas
WHERE edad > 40
ORDER BY dni ASC
```
````

---

## Ejercicio 2

Mostrar todas las personas que se llaman `ANTONIO` o `PEDRO` ordenadas por edad.

````{admonition} Solución
:class: dropdown
```sql
SELECT * FROM PERSONAS
WHERE ((nombre = 'Pedro') OR (nombre = 'Antonio'))
ORDER BY edad
```
````

---

## Ejercicio 3

Insertar una nueva persona en la base de datos y verificar que se ha realizado con éxito realizando una consulta.

````{admonition} Solución
:class: dropdown
```sql
INSERT INTO personas
VALUES (5, 'Fernando', 'Santa Rita', 'Vizuet', 315268463, 23, 'CDMX', NULL)
```
````

---

## Ejercicio 4

Actualizar el registro anteriormente creado porque Fernando tenía 24 años en lugar de 23.

````{admonition} Solución
:class: dropdown
```sql
UPDATE personas
SET edad = 24
WHERE nombre = 'Fernando'
```
````

---

## Ejercicio 5

Borrar el último registro actualizado realizando la selección por el nombre y los dos apellidos.

````{admonition} Solución
:class: dropdown
```sql
DELETE FROM personas
WHERE nombre = 'Fernando'
AND apellido1 = 'Santa Rita'
AND apellido2 = 'Vizuet'
```
````

---

## Ejercicio 6

Seleccionar que tipo de productos hemos vendido

````{admonition} Solución
:class: dropdown
```sql
SELECT DISTINCT producto FROM pedidos
```
````