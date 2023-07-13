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

# Ejercicio: SQL avanzado

## 🔘 Ejercicio 1

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



