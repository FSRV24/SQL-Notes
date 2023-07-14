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

# 🎭 SQL avanzado

## 🔘 LIMIT

Establece el número de filas a visualizar.

**Sintaxis**

```sql
SELECT * FROM [table_name] LIMIT [no_filas]
```

## 🔘 LIKE

Permite el uso de expresiones regulares.

**Sintaxis**

```sql
-- registro que comience en CIA
SELECT * FROM [table_name] WHERE [column1] LIKE ['CIA%']

-- registro que termine en CIA
SELECT * FROM [table_name] WHERE [column1] LIKE ['%CIA']

-- registro que contenga CIA
SELECT * FROM [table_name] WHERE [column1] LIKE ['%CIA%']
```

## 🔘 IN

Búsqueda en valores en listas.

**Sintaxis**

```sql
SELECT * FROM [table_name] WHERE [col] IN (val1, val2, ...)
```

## 🔘 BETWEEN

Búsqueda en valores en intervalos.

**Sintaxis**

```sql
SELECT * FROM [table_name]
WHERE [column] BETWEEN [val1] AND [val2]
```

## 🔘 ALIAS

Renombra las columnas para su uso dentro del script o de la consulta, pero no es un cambio permanente.

**Sintaxis**

```sql
SELECT [column1] AS [alias] FROM [table_name]
```

## 🔘 JOIN

Permite concatenar tablas horizontalmente a través de atributos compartidos como llaves.

**Sintaxis**

```sql
SELECT * FROM [table1] JOIN [table2] WHERE table1.col = table2.col
```

## 🔘 UNION

Permite unir dos sentencias SELECT, donde los resultados se concatenan verticalmente, se requiere que haya el mismo número de columnas, en el mismo orden, y que cada columna sea del mismo tipo de dato.

**Sintaxis**

```sql
SELECT * FROM [table_name] WHERE [column1] > [val]
UNION
SELECT * FROM [table_name] WHERE [column2] = [val]
```

## 🔘 CREATE TABLE

Crea tablas dentro de la base de datos.

**Sintaxis**

```sql
CREATE TABLE [table_name] (column1 datatype, column2 datatype, column1 datatype)
```

Se tienen los siguientes tipos de datos:

- **Números enteros:**
  - `INTEGER`: números enteros con signo.
  - `SMALLINT`: enteros pequeños con signo.
  - `BIGINT`: enteros grandes con signo.

- **Números decimales:**
  - `DECIMAL(p, s)`: números decimales de precisión fija, donde "p" representa la precisión total y "s" es la escala decimal (número de dígitos a la derecha del punto decimal).
  - `NUMERIC(p, s)`: similar a DECIMAL, pero puede almacenar números con decimales.
  - `FLOAT`: números de coma flotante.
  - `REAL`: números de coma flotante de precisión simple.
  - `DOUBLE PRECISION`: números de coma flotante de doble precisión.

- **Cadenas de caracteres:**
  - `CHAR(n)`: cadena de caracteres de longitud fija con una longitud máxima de "n".
  - `VARCHAR(n)`: cadena de caracteres de longitud variable con una longitud máxima de "n".
  - `TEXT`: cadena de caracteres de longitud variable sin límite específico.

- **Fechas y horas:**
  - `DATE`: fecha sin la parte del tiempo.
  - `TIME`: hora sin la parte de la fecha.
  - `TIMESTAMP`: fecha y hora combinadas.

- **Booleano:**
  - `BOOLEAN`: representa los valores verdadero (TRUE) y falso (FALSE).

## 🔘 NOT NULL

En la creación de una tabla, establece que los valores de una columna no puede tener valores nulos.

**Sintaxis**

```sql
CREATE TABLE [table_name] (column1 datatype NOT NULL)
```

También, a través del filtrado con `WHERE`, se pueden obtener las instancias que contengan valores nulos.

```sql
-- valores nulos
SELECT * FROM [table_name] WHERE [column] IS NULL

-- valores no nulos
SELECT * FROM [table_name] WHERE [column] IS NOT NULL
```

## 🔘 UNIQUE

En la creación de una tabla, establece que los valores en una columna no pueden repetirse.

**Sintaxis**

```sql
CREATE TABLE [table_name] (column1 datatype UNIQUE)
```

```{admonition} Llaves primarias *vs* llaves foráneas
:class: info
Las **llaves primarias** son un identificador único de las instancias dentro de una tabla, no puede tener valores nulos, y garantiza la unicidad e integridad de los datos. Se utiliza a su vez para establecer relaciones entre otras tablas, esto a través de las **llaves foráneas**, atributos que permiten la relación con el resto de tablas.

Las **relaciones entre tablas** pueden ser:

- Uno a muchos `[1:N]`
- Muchos a muchos `[N:N]`

También, diferentes atributos se pueden combinar para formar **llaves compuestas**.
```

Podemos entonces establecer **llaves primarias**:

```sql
CREATE TABLE [table_name] (col_id INTEGER PRIMARY KEY)
```

También **llaves foráneas** para indicar la llave primaria de otra tabla:

````{margin}
```{note}
Al momento de insertar un nuevo registro en los campos indicados como *llaves foráneas*, los valores deberán pertenecer al dominio de dicho campo en la otra tabla.
```
````

```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
    ...
    FOREIGN KEY (column_name) REFERENCES referenced_table(referenced_column)
);
```

La columna `column_name` hace referencia a una de las columnas de la tabla que está siendo creada, no significa que en la misma línea se esté creando una nueva variable.

## 🔘 CHECK

Establece restricciones en los campos de una tabla al crear una tabla.

**Sintaxis**

```sql
CREATE TABLE [table_name] (
    column1 datatype,
    column2 datatype,
    ...
    CHECK (column1 > 0)
);
```

Hasta ahora, las condiciones `CHECK` solo establecen comparaciones entre valores numéricos.

## 🔘 CREATE INDEX

Se crea un índice hash dada cierta columna. Devuelve resultados de búsqueda de forma instantanea, con complejidad $O(1)$, pero es recomdable hacerlo con parámetros de búsqueda como identificadores o llaves primarias.

**Sintaxis**

```sql
CREATE INDEX [index_name] ON [table_name] (column1, column2, ...);
```

## 🔘 DROP

Sirve para eliminar tablas, índices o una base de datos.

**Sintaxis**

```sql
DROP INDEX [index_name]
DROP TABLE [table_name]
```

## 🔘 TRUNCATE

Elimina los datos pero no la estructura de la tabla.

**Sintaxis**

```sql
TRUNCATE TABLE [table_name]
```

## 🔘 ALTER

Añade, elimina, o modifica columnas de una tabla.

**Sintaxis**

```sql
-- añadir columna
ALTER TABLE [table_name] ADD [column datatype];

-- eliminar columna
ALTER TABLE [table_name] DROP COLUMN [column_name];

-- añadir constricciones, por ejemplo, una llave primaria
ALTER TABLE [table_name]
ADD CONSTRAINT [constraint_name] PRIMARY KEY (column1, column2, ...);

-- eliminar constricciones
ALTER TABLE [table_name]
DROP CONSTRAINT [constraint_name];
```

```{admonition} Constricciones
:class: info
Las constricciones que maneja SQL son:

- `PRIMARY KEY`
- `FOREIGN KEY`
- `UNIQUE`
- `CHECK`
- `NOT NULL`

Todas estas pueden ser modificadas después de la creación de la tabla.
```

## 🔘 AUTOINCREMENT

Genera números únicos de forma automática y secuencial en la creación de una tabla.

**Sintaxis**

````{margin}
```{tip}
Para un mejor orden, los campos autoincrementales suelen estar el principio del resto de campos.
```
````

```sql
CREATE TABLE [table_name] (
    column_id INTEGER PRIMARY KEY AUTOINCREMENT,
    column1 datatype,
    column2 datatype,
    ...
);
```

Al momento de agregar nuevas instancias, ignoramos el lugar del campo incremental y se añade el resto de campos.


## 🔘 CREATE VIEW

Crea una tabla temporal, subconjunto de otra tabla.

**Sintaxis**

```sql
-- crea la vista temporal
CREATE VIEW [name_view]
AS SELECT [column1, column2, ...]
FROM [table_name]
WHERE [condition]

-- elimina la vista temporal
DROP VIEW [name_view]
```

## 🔘 Funciones de agregación

Aplica funciones de agregación sobre el atributo indicado.

```sql
SELECT [funcion(column_name)] FROM [table_name]
```

Las funciones de agregación pueden ser:

- `SUM`
- `AVG`
- `COUNT`
- `MAX`
- `MIN`
- 
```{tip}
La función de agregación `COUNT` suele ser combinada con el statement `WHERE`, para contabilizar registros que cumplan cierta condición.
```

## 🔘 CURRENT TIME, CURRENT DATE

Permite obtener la hora independiente a cualquier tabla en la base de datos.

**Sintaxis**

```sql
SELECT CURRENT_TIME AS [hour]

-- combinar resultados con la hora de consulta
SELECT [column1, column 2, ...], CURRENT_TIME AS [hour] FROM [table_name]
```

De modo similar, la fecha puede ser incluida en las consultas o de forma independiente a estas.

```sql
SELECT CURRENT_DATE AS [date]

-- combinar resultados con la fecha de consulta
SELECT [column1, column2, ...], CURRENT_DATE AS [date] FROM [table_name] 
```

La combinación de fecha y hora se da a través de `CURRENT_TIMESTAMP` de modo completamente análogo.