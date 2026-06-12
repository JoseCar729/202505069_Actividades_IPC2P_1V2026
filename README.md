# Actividad de Investigación y Práctica
## Estructuras de Datos Avanzadas y APIs con ASP.NET Core

**Nombre:** Jose Carlos González López  
**Carnet:** 202505069  
**Curso:** Laboratorio de Introducción a la Programación y Computación 2  
**Fecha:** 11/06/2026

---
## 1. Estructuras de Datos Eficientes

### Árboles Binarios de Búsqueda (ABB)

Un Árbol Binario de Búsqueda (ABB) es una estructura de datos jerárquica en la que cada nodo puede tener como máximo dos hijos. Su principal característica es que mantiene un orden específico entre los elementos almacenados.

#### Regla de ordenamiento

* Todos los valores del subárbol izquierdo de un nodo deben ser menores que el valor del nodo.
* Todos los valores del subárbol derecho de un nodo deben ser mayores que el valor del nodo.

Gracias a esta propiedad, las operaciones de búsqueda pueden realizarse de manera más eficiente que en una lista lineal.

#### Desventaja

La principal desventaja de un ABB ocurre cuando los datos se insertan en un orden secuencial (por ejemplo: 1, 2, 3, 4, 5). En este caso, el árbol se vuelve desbalanceado y adquiere una forma similar a una lista enlazada.

Cuando esto sucede, la complejidad de búsqueda, inserción y eliminación puede degradarse de **O(log n)** a **O(n)**, reduciendo considerablemente la eficiencia de la estructura.

---

### Árboles AVL

Un árbol AVL es un Árbol Binario de Búsqueda auto-balanceado. Fue diseñado para evitar los problemas de desbalance que pueden presentarse en un ABB tradicional.

#### Factor de balanceo

El factor de balanceo de un nodo se calcula mediante la siguiente fórmula:

**Factor = AlturaIzquierda − AlturaDerecha**

Para que el árbol permanezca balanceado, el factor de balanceo de cada nodo debe ser:

* -1
* 0
* 1

Cuando el factor de balanceo supera estos límites, el árbol realiza rotaciones automáticamente para recuperar el equilibrio.

#### Complejidad

Debido a que el árbol mantiene una altura controlada mediante rotaciones, las operaciones fundamentales conservan una complejidad de:

* Búsqueda: **O(log n)**
* Inserción: **O(log n)**
* Eliminación: **O(log n)**

Esto garantiza un rendimiento eficiente incluso cuando se manejan grandes cantidades de datos.

---

## 2. Fundamentos de Web APIs

### ¿Qué es una API?

Una API (Application Programming Interface) es un conjunto de reglas y mecanismos que permite la comunicación entre diferentes aplicaciones o sistemas de software.

Las Web APIs utilizan generalmente el modelo Cliente-Servidor:

1. El cliente envía una petición (Request) al servidor.
2. El servidor procesa la solicitud.
3. El servidor devuelve una respuesta (Response) al cliente.

La comunicación se realiza normalmente mediante el protocolo HTTP.

### Funcionamiento de una petición y respuesta HTTP

Una petición HTTP contiene información como:

* URL del recurso solicitado.
* Método HTTP utilizado.
* Encabezados (Headers).
* Datos enviados en el cuerpo de la petición (Body), cuando corresponda.

Después de procesar la solicitud, el servidor devuelve una respuesta HTTP que incluye:

* Un código de estado.
* Encabezados.
* Los datos solicitados o el resultado de la operación.

Por ejemplo, una petición para obtener una lista de nodos puede devolver un código **200 OK** junto con un documento JSON que contiene los datos.

---

### Verbos HTTP

#### GET

El método **GET** se utiliza para recuperar información existente en el servidor.

Características:

* Obtiene recursos sin modificarlos.
* No altera el estado de la aplicación.
* Es un método idempotente.

Un ejemplo sería solicitar la lista de nodos almacenados en una API.

#### POST

El método **POST** se utiliza para crear nuevos recursos en el servidor.

Características:

* Permite enviar datos para su almacenamiento.
* Modifica el estado de la aplicación.
* No es idempotente.

Por ejemplo, al enviar varias veces la misma petición POST para crear un nodo, se pueden generar múltiples registros nuevos.
