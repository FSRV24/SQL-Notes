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

# SQL Básico

## Select

Permite realizar consultas sobre las columnas de una tabla en una base de datos.

**Sintaxis**

```sql
SELECT [col1, col2, ...] FROM [table_name]
```

```{tip}
Si se utiliza `*` en lugar del nombre de alguna(s) columna(s), entonces se devuelven todos los atributos de la tabla.
```

## Distinct

Se utiliza para devolver valores únicos.

**Sintaxis**

```sql
SELECT [DISTINCT col1, col2, DISTINCT col3] FROM [table_name]
```

```{note}
En pandas se emplea el método `unique()` o `nunique()` para reazalizar conteos.
```

## Where

Se emplea para imponer filtros en la consulta.

**Sintaxis**

```sql
SELECT [nombre] FROM [personas] WHERE [nombre = "Luis"]
SELECT * FROM [personas] WHERE [edad > 30]
SELECT [nombre] FROM [personas] WHERE [apellido1 = 'Perez', edad > 50]
```

```{tip}
Se pueden emplear comillas simples o dobles.
```

## Operadores AND y OR

Se emplean para encadenar condiciones dentro del dominio de `WHERE`.

**Sintaxis**

```sql
SELECT * FROM [personas] WHERE [nombre = 'Antonio'] AND [apellido1 = 'Perez']
```

## Order by

Se hacen ordenamientos respecto a una columna. El ordenamiento por default es *ascendente*.

**Sintaxis**

```sql
SELECT [nombre] FROM [personas] ORDER BY [edad]
SELECT [nombre] FROM [personas] ORDER BY [edad] DESC
```

```{note}
Las columnas de tipo `string` se ordenan por orden alfabético si son utilizadas como criterio de ordenamiento.
```

## Insert into

Se emplea para incluir nuevas instancias en una tabla.

**Sintaxis**

```sql
INSERT INTO [table_name] VALUES (5, 'Marta', 'Santos', 'Perez', 33)
```

Siempre se deben agregar los datos de forma íntegra, respetando el tipado de cada columna.

## Update

````{margin}
```{warning}
Hay que especificar en su totalidad los registros en la tabla para que no haya errores en la actualización.
```
````

Cambia valores en lugar específicos de una tabla.

**Sintaxis**

```sql
UPDATE [table_name] SET [col1] = [val1] WHERE [col2] = [val2]
```

## Delete

Elimina filas especificadas.

**Sintaxis**

```sql
DELETE FROM [table_name] WHERE [col] = [val]
```