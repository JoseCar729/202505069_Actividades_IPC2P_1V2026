# Parte 1: Investigación Teórica y Análisis de Casos

## 1. El Límite de las Rotaciones Simples y Desbalanceo en "Zig-Zag"

### El Problema Cruzado

Las rotaciones simples en árboles AVL no siempre son suficientes para corregir un desbalance. Esto ocurre cuando la inserción genera una estructura cruzada o tipo **Zig-Zag**, como en la secuencia de inserción **30, 10, 20**.

El árbol resultante es:

```text
    30
   /
 10
   \
    20
```

En este caso, el nodo 30 se encuentra desbalanceado hacia la izquierda, mientras que su hijo izquierdo (10) está inclinado hacia la derecha. Si se aplicara únicamente una rotación simple, el problema no se resolvería correctamente y el árbol continuaría desbalanceado.

La **Rotación Doble Izquierda-Derecha (RID)** se ejecuta cuando:

* El Factor de Equilibrio del nodo padre es **-2**.
* El Factor de Equilibrio de su hijo izquierdo es **+1**.

Matemáticamente:

```text
FE(Padre) = -2
FE(Hijo Izquierdo) = +1
```

La corrección se realiza en dos pasos:

1. Rotación simple a la izquierda sobre el hijo izquierdo.
2. Rotación simple a la derecha sobre el nodo desbalanceado.

El resultado final es:

```text
    20
   /  \
 10   30
```

De esta manera, el árbol recupera su equilibrio.

### Principio DRY (Don't Repeat Yourself)

El principio DRY establece que no debe duplicarse código que realiza la misma tarea. En el caso de los árboles AVL, las rotaciones dobles (RID y RDI) pueden implementarse reutilizando las rotaciones simples ya existentes.

Las ventajas de esta estrategia son:

* Menor cantidad de código.
* Mayor facilidad de mantenimiento.
* Menor probabilidad de errores al manipular referencias o punteros.
* Mejor reutilización de componentes ya probados.
* Mayor claridad en la implementación.

Por esta razón, una rotación doble suele construirse combinando dos rotaciones simples en lugar de reescribir toda la lógica desde cero.

---

## 2. Fundamentos de Arquitectura Web y Protocolo HTTP

### El Modelo Cliente-Servidor

El modelo cliente-servidor es una arquitectura donde un cliente solicita servicios o recursos a un servidor.

Los componentes principales son:

* **Cliente:** navegador web, aplicación móvil o cualquier software consumidor.
* **Servidor:** aplicación que procesa las solicitudes y genera respuestas.

El flujo de comunicación es:

```text
Cliente --> HTTP Request --> Servidor
Cliente <-- HTTP Response -- Servidor
```

La petición (**Request**) normalmente contiene:

* Método HTTP.
* URL del recurso solicitado.
* Encabezados (Headers).
* Datos opcionales (Body).

La respuesta (**Response**) contiene:

* Código de estado HTTP.
* Encabezados.
* Datos solicitados o resultado de la operación.

Los datos viajan a través de la red utilizando el protocolo HTTP.

### Semántica de Operaciones

#### Método GET

El método **GET** se utiliza para recuperar información existente en el servidor.

Características:

* No modifica datos.
* Es seguro para consultas.
* Puede ejecutarse varias veces sin alterar el estado del sistema.

Ejemplo:

```http
GET /api/arbol
```

Este método se utiliza para obtener la estructura actual del árbol.

#### Método POST

El método **POST** se utiliza para enviar información al servidor con el objetivo de crear o modificar recursos.

Características:

* Modifica el estado del sistema.
* Puede crear nuevos recursos.
* Generalmente responde con el código HTTP **201 Created** cuando la operación es exitosa.

Ejemplo:

```http
POST /api/arbol/insertar
```

Este método se utiliza para insertar nuevos nodos o realizar cambios en la estructura de datos.

### Diferencia entre GET y POST

| Método | Propósito                                          |
| ------ | -------------------------------------------------- |
| GET    | Recuperar información o consultar datos existentes |
| POST   | Insertar, crear o modificar información            |

Por lo tanto, en la API desarrollada para esta práctica:

* **GET** se utiliza para recuperar la estructura actual del árbol AVL.
* **POST** se utiliza para insertar un nodo y simular el proceso de balanceo compuesto.

```
```
