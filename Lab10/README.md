# Code Optimization Lab Report

### Provided Code Snippets

**JavaScript Snippet:**

```javascript
// Inefficient loop handling and excessive DOM manipulation
function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  for (let i = 0; i < items.length; i++) {
    let listItem = document.createElement("li");
    listItem.innerHTML = items[i];
    list.appendChild(listItem);
  }
}
```

**Java Snippet:**

```java
// Redundant database queries
public class ProductLoader {
    public List<Product> loadProducts() {
        List<Product> products = new ArrayList<>();
        for (int id = 1; id <= 100; id++) {
            products.add(database.getProductById(id));
        }
        return products;
    }
}
```

**C# Snippet:**

```csharp
// Unnecessary computations in data processing
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>();
    foreach (var d in data) {
        if (d % 2 == 0) {
            result.Add(d * 2);
        } else {
            result.Add(d * 3);
        }
    }
    return result;
}
```
---

## Análisis del Código

### Análisis del Fragmento de JavaScript

#### Problemas Potenciales:
1. **Ineficiencia en el Manejo de Bucles:** El bucle crea y añade elementos DOM uno por uno, causando múltiples reflows y repaints en el navegador.
2. **Manipulación Excesiva del DOM:** Manipular el DOM directamente dentro del bucle puede ser costoso en términos de rendimiento.

### Análisis del Fragmento de Java

#### Problemas Potenciales:
1. **Consultas Redundantes a la Base de Datos:** El bucle realiza una consulta separada a la base de datos por cada producto, llevando a 100 consultas para 100 productos.
2. **Recuperación Ineficiente de Datos:** Recuperar cada producto individualmente es menos eficiente que la obtención en bloque.

### Análisis del Fragmento de C#

#### Problemas Potenciales:
1. **Cálculos Innecesarios:** El cálculo dentro del bucle puede optimizarse.
2. **Procesamiento Ineficiente de Datos:** El bucle procesa cada punto de datos individualmente sin ningún intento de optimizar la operación.

## Implementación de Optimizaciones

### Fragmento de JavaScript Optimizado

#### Código Optimizado:
```javascript
function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  let fragment = document.createDocumentFragment();
  items.forEach(item => {
    let listItem = document.createElement("li");
    listItem.innerHTML = item;
    fragment.appendChild(listItem);
  });
  list.appendChild(fragment);
}
```

- Reemplazo del bucle `for` con `forEach` para mayor legibilidad.
- Uso de un `DocumentFragment` para agrupar las actualizaciones del DOM, reduciendo reflows y repaints.

### Fragmento de Java Optimizado

#### Código Optimizado:
```java
public class ProductLoader {
    public List<Product> loadProducts() {
        return database.getProductsByIds(IntStream.rangeClosed(1, 100).boxed().collect(Collectors.toList()));
    }
}
```
- Uso de `getProductsByIds` para obtener todos los productos en una sola consulta.
- Obtención en bloque de los productos para reducir el número de consultas de 100 a 1.

### Fragmento de C# Optimizado

#### Código Optimizado:
```csharp
public List<int> ProcessData(List<int> data) {
    return data.Select(d => d % 2 == 0 ? d * 2 : d * 3).ToList();
}
```
- Uso de LINQ para simplificar la lógica de procesamiento de datos.
- Reducción de la complejidad del bucle usando `Select` y `ToList` para un procesamiento de datos más eficiente.

Estas optimizaciones no solo mejoran el rendimiento de los fragmentos de código, sino que también aumentan la legibilidad y mantenibilidad del código. Al aplicar técnicas de optimización a nivel de código, hemos reducido la carga computacional y mejorado la eficiencia general de las aplicaciones.
