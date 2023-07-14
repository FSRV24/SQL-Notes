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

Seleccionar los pedidos con importes entre 100 y 500.

````{admonition} Solución
:class: dropdown
```sql
SELECT *
FROM pedidos
WHERE importe BETWEEN 100 AND 500;
```
````

---

## Ejercicio 2

Seleccionar el nombre, el primer apellido y la edad de las personas que en el primer apellido tengan la letra `Z`.

````{admonition} Solución
:class: dropdown
```sql
SELECT nombre, apellido1, edad
FROM personas
WHERE apellido1 LIKE '%Z%';
```
````

---

## Ejercicio 3

Seleccionar el nombre, el primer apellido, edad y el departamento de las personas cuyo nombre sea `ANTONIO` y el resultado ordenarlo por departamento.

````{admonition} Solución
:class: dropdown
```sql
SELECT nombre, apellido1, edad, departamento
FROM personas JOIN departamentos
WHERE personas.dep = departamentos.dep AND nombre = 'Antonio'
ORDER BY departamento
```
````

---

## Ejercicio 4

De la tabla de pedidos, selecciona los pedidos de impresoras y los pedidos con un importe mayor de 500 utilizando la sentencia `UNION`.

````{admonition} Solución
:class: dropdown
```sql
SELECT *
FROM pedidos
WHERE producto = 'impresora'
UNION
SELECT *
FROM pedidos
WHERE importe > 500
```
````

---

## Ejercicio 5

Selecciona los pedidos cuyo importe sea mayor que el importe medio de todos los pedidos.

````{admonition} Solución
:class: dropdown

La solución posiblemente sea incorrecta, pero como una idea a futuro podemos pensar en crear una tabla temporal y luego utilizarla con la siguiente query, esto con la idea de crear variables como lo haríamos en un lenguaje de programación convencional.

```sql
SELECT * 
FROM pedidos 
WHERE importe > AVG(importe)
```
````

---

## Ejercicio 6

Seleccionar el número de personas que tienen menos de 50 años.

````{admonition} Solución
:class: dropdown

Asumimos que lo que se busca es contar el número de instancias con la condición establecida.

```sql
SELECT COUNT(*)
FROM personas
WHERE edad < 50
```
````

---

## Ejercicio 7

Seleccionar los 2 primeros pedidos que tengan un importe mayor de 80 euros.

````{admonition} Solución
:class: dropdown
```sql
SELECT * 
FROM pedidos
WHERE importe > 80
LIMIT 2
```
````

---

## Ejercicio 8

Seleccionar aquellos pedidos que tengan un importe de 150, 500 o 600 y ordenarlos por importe.

````{admonition} Solución
:class: dropdown
```sql
SELECT *
FROM pedidos 
WHERE importe IN (150, 500, 600)
ORDER BY importe
```
````

---

## Ejercicio 9

Crear una nueva tabla de nombre `TABLA2`. Incluir dos columnas:

- Primera columna con nombre `ID` y de tipo numérico entero
- Segunda columna con nombre `DATOS` de tipo texto

````{admonition} Solución
:class: dropdown
```sql
CREATE TABLE TABLA2 (
  ID INTEGER,
  DATOS TEXT
)
```
````

---

## Ejercicio 10

Insertar dos nuevas filas en nuestra nueva tabla `TABLA2`.

````{admonition} Solución
:class: dropdown
```sql
INSERT INTO TABLA2
VALUES(1, 'Primera instancia');

INSERT INTO TABLA2
VALUES(2, 'Segunda instancia');
```
````

---

## Ejercicio 11

Borrar todos los registros de nuestra `TABLA2`, pero sin eliminar la estructura.

````{admonition} Solución
:class: dropdown
```sql
TRUNCATE TABLE TABLA2
```
````

---

## Ejercicio 12

Borrar definitivamente la tabla `TABLA2`.

````{admonition} Solución
:class: dropdown
```sql
DROP TABLE TABLA2
```
````

---

## Ejercicio 13

Crear una tabla `SALARIOS` con los siguientes campos:

- `ID`: Número entero, autoincremental y clave primaria de la tabla
- `NOMBRE`: Texto que no permita valores nulos
- `EDAD`: Número entero y no se permiten valores nulos
- `DIRECCION`: Texto de 50 posiciones
- `SALARIO`: Número con decimales

````{admonition} Solución
:class: dropdown
```sql
CREATE TABLE SALARIOS (
  ID INTEGER PRIMARY KEY AUTOINCREMENT,
  NOMBRE TEXT NOT NULL,
  EDAD SMALLINT NOT NULL,
  DIRECCION VARCHAR(50),
  SALARIO REAL
)
```
````

---

## Ejercicio 14

Insertar en la tabla `SALARIOS` dos instancias con los siguientes datos:

- `NOMBRE = 'Antonio', EDAD = 30, DIRECCION = 'calle 1', SALARIO = 2000.00`
- `NOMBRE = 'Juan', EDAD = 40, DIRECCION = 'calle 2', SALARIO = 3000.00`

````{admonition} Solución
:class: dropdown
```sql
INSERT INTO SALARIOS (NOMBRE, EDAD, DIRECCION, SALARIO)
VALUES ('Antonio', 30, 'calle 1', 2000.00);

INSERT INTO SALARIOS (NOMBRE, EDAD, DIRECCION, SALARIO)
VALUES ('Juan', 40, 'calle 2', 3000.00);
```
````

---

## Ejercicio 15

Modificar el tipo de dato de una columna.

1. Renombrar la tabla `SALARIOS` con el nombre `SALARIOS2`
2. Crear una nueva tabla `SALARIOS` con los campos:
   - `ID`: Entero, clave primaria y autoincremental
   - `NOMBRE`: Texto no nulo
   - `EDAD`: Entero
   - `DIRECCION`: Texto variable de 50 posiciones
   - `SALARIO`: Entero
3. Copiar los datos de la tabla `SALARIOS2` en la nueva tabla `SALARIOS`

````{admonition} Solución
:class: dropdown
```sql
-- 1)
ALTER TABLE SALARIOS RENAME TO SALARIOS2;

-- 2)
CREATE TABLE SALARIOS (
  ID INTEGER PRIMARY KEY AUTOINCREMENT,
  NOMBRE TEXT NOT NULL,
  EDAD INTEGER,
  DIRECCION VARCHAR(50),
  SALARIO INTEGER
);

-- 3)
INSERT INTO SALARIOS (NOMBRE, EDAD, DIRECCION, SALARIO)
SELECT NOMBRE, EDAD, DIRECCION, SALARIO FROM SALARIOS2;
```
````

---

## Ejercicio 16

Dada la tabla `personas`, seleccionar los dos últimos registros.

````{admonition} Solución
:class: dropdown
```sql
SELECT *
FROM personas
ORDER BY id DESC
LIMIT 2
```
````

---

## Ejercicio 17

Obtener el importe total de los pedidos agrupados por producto. Por cada producto de la tabla `PEDIDOS`, calcular la suma de sus importes. Renombrar la columna que suma los importes como `IMPORTE_TOTAL`.

````{admonition} Solución
:class: dropdown
```sql
SELECT producto, SUM(importe) AS IMPORTE_TOTAL
FROM pedidos
GROUP BY producto
```
````

---

## Ejercicio 18

Seleccionar aquellas personas cuyo salario es mayor a 4000.

1. Insertar una nueva persona en la tabla `SALARIOS`:
   - `ID = 3, NOMBRE = 'MARTA', EDAD = 40, DIRECCION = 'calle 3', SALARIO = 5000`
2. Seleccionar los nombres de los salarios mayores de 4000.
3. Seleccionar las personas cuyo nombre esté en la selección anterior.

````{admonition} Solución
:class: dropdown
```sql
-- 1)
INSERT INTO SALARIOS (ID, NOMBRE, EDAD, DIRECCION, SALARIO)
VALUES (3, 'Marta', 40, 'calle 3', 5000);

-- 2)
SELECT nombre
FROM SALARIOS
WHERE salario > 4000;

-- 3)
SELECT * FROM PERSONAS
WHERE nombre = (SELECT nombre FROM SALARIOS WHERE salario > 4000)
```
````

---

## Ejercicio 19

Realizar en una misma consulta la selección de los nombres de las personas que cumplan alguna de las 2 siguientes condiciones:

1. Personas menores de 30 años
2. Personas cuyo salario sea mayor de 2500 y menor de 4000

````{admonition} Solución
:class: dropdown
```sql
SELECT nombre FROM personas WHERE edad < 30
UNION
SELECT nombre FROM SALARIOS WHERE salario BETWEEN 2500 AND 4000
```
````

---

## Ejercicio 20

Crear una consulta que devuelva en una sola consulta el nombre y los dos apellidos concatenados y separados por espacios. Ordenar el resultado por esta nueva columna que se llamará `PERSONA`.

````{admonition} Solución
:class: dropdown
```sql
SELECT nombre || ' ' || apellido1 || ' ' || apellido2 as PERSONA
FROM personas
ORDER BY PERSONA
```
````

---

## Ejercicio 21

Crear la tabla `visitas` que tiene que almacenar para cada visita los siguientes campos:

- Nombre y teléfono de la persona que visita la tienda, la fecha, hora de comienzo y hora de finalización de la visita

Además, le primer campo de la tabla es `id_visita` de tipo entero, autoincremental y clave primaria de la tabla.

````{admonition} Solución
:class: dropdown
```sql
CREATE TABLE visitas (
  id_visita INTEGER PRIMARY KEY AUTOINCREMENT,
  nombre TEXT NOT NULL,
  telefono INTEGER,
  fecha DATE NOT NULL,
  hora_inicio TIME NOT NULL,
  hora_fin TIME NOT NULL
)
```
````

---

## Ejercicio 22

Insertar dos nuevos registros en la tabla `visitas`:

- Pueden tener cualquier valor
- Recuerden que el primer campo es autoincremental

````{admonition} Solución
:class: dropdown
```sql
INSERT INTO visitas (nombre, telefono, fecha, hora_inicio, hora_fin)
VALUES(
  'Fernando',
  5512345678,
  '2023-07-14',
  '16:25:00',
  '18:23:00'
)
```
````

---

## Ejercicio 23

Realizar las siguientes consultas sobre la tabla `visita`:

1. Buscar las visitas con fechas anteriores al 28 de octubre de 2022
2. Buscar las visitas realizadas entre los días 25 y 30 de octubre de 2022

````{admonition} Solución
:class: dropdown
```sql
-- consulta 1
SELECT *
FROM visitas
WHERE fecha <= '2022-10-28';

-- consulta 2
SELECT *
FROM visitas
WHERE fecha BETWEEN '2022-10-25' AND '2022-10-30'
```
````