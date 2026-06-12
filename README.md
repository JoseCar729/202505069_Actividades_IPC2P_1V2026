# Actividad2_IPC2P_1V2026
Parte 1: Investigación Teórica
1. Estructuras de Datos Eficientes
Árboles Binarios de Búsqueda (ABB)

Un Árbol Binario de Búsqueda (ABB) es una estructura de datos jerárquica donde cada nodo puede tener como máximo dos hijos.

Reglas de ordenamiento:

Todos los valores del subárbol izquierdo son menores que el valor del nodo padre.
Todos los valores del subárbol derecho son mayores que el valor del nodo padre.

Ejemplo:

        10
       /  \
      5    15
Desventaja

Si los datos se insertan en orden secuencial (por ejemplo: 1, 2, 3, 4, 5), el árbol se degenera y se comporta como una lista enlazada.

1
 \
  2
   \
    3
     \
      4
       \
        5

En este caso las búsquedas dejan de ser eficientes, pasando de O(log n) a O(n).

Árboles AVL

Un árbol AVL es un árbol binario de búsqueda auto-balanceado.

Su objetivo es mantener una altura equilibrada para garantizar operaciones eficientes.

Factor de Balanceo

Se calcula mediante:

Factor=Altura
Izquierda
	​

−Altura
Derecha
	​


Los valores permitidos son:

-1
0
1

Si el factor de balanceo supera estos límites, se realizan rotaciones para reequilibrar el árbol.

Complejidad

Gracias al balance automático:

Operación	Complejidad
Búsqueda	O(log n)
Inserción	O(log n)
Eliminación	O(log n)

Esto se debe a que la altura del árbol siempre permanece cercana a log₂(n).

2. Fundamentos de Web APIs
¿Qué es una API?

Una API (Application Programming Interface) es un conjunto de reglas que permite que diferentes aplicaciones se comuniquen entre sí.

En una Web API se utiliza el modelo Cliente-Servidor:

El cliente envía una petición (Request).
El servidor procesa la solicitud.
El servidor devuelve una respuesta (Response).

Ejemplo:

Cliente (Postman/Navegador)
          |
          | HTTP Request
          v
       Servidor
          |
          | HTTP Response
          v
       Cliente
Funcionamiento mediante HTTP
Request

Contiene:

URL
Método HTTP
Encabezados (Headers)
Cuerpo (Body) opcional

Ejemplo:

POST /api/nodos
Response

Contiene:

Código de estado
Encabezados
Datos solicitados

Ejemplo:

200 OK
Verbos HTTP
GET

Se utiliza para recuperar información.

Ejemplo:

GET /api/nodos

Características:

No modifica datos.
Es idempotente.

Una petición GET repetida varias veces produce el mismo resultado.

POST

Se utiliza para crear recursos nuevos.

Ejemplo:

POST /api/nodos

Características:

Agrega nuevos datos.
No es idempotente.

Si se ejecuta varias veces, se crean varios recursos.
