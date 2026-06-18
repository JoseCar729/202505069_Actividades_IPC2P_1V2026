# Actividad de Laboratorio: Arquitectura Multi-Nivel (N-Tier) y Patrón MVC en .NET

**Nombre:** Jose Carlos González López
**Curso:** Laboratorio de Introducción a la Programación y Computación 2
**Fecha:** 17 de junio de 2026

---

# Parte 1: Fundamentación Teórica y Análisis Crítico

## 1. El Tránsito hacia los Sistemas Distribuidos y Multi-Capa

### La Limitación del Monolito Local

Cuando la interfaz de usuario, la lógica de negocio y la base de datos se encuentran alojadas en una sola máquina física, el sistema presenta limitaciones significativas de escalabilidad y disponibilidad. Los usuarios dependen de un único equipo para acceder a la información, lo que dificulta el crecimiento del sistema y genera riesgos de pérdida de servicio ante fallos de hardware. Además, la sincronización de datos entre múltiples usuarios se vuelve compleja y poco eficiente.

### Distinción Crítica (Layers vs. Tiers)

Las **capas lógicas (Layers)** representan la organización interna del software según sus responsabilidades, como presentación, lógica de negocio y acceso a datos.

Los **niveles físicos (Tiers)** representan la distribución física de estas capas en diferentes servidores o equipos dentro de una infraestructura.

Por lo tanto, las capas son una división conceptual del software, mientras que los niveles corresponden a la distribución física de los componentes del sistema.

### Responsabilidades en la Arquitectura de 3 Niveles

#### Nivel 1: Capa de Presentación (Presentation Tier)

Su función principal es interactuar con el usuario, mostrar información y capturar datos de entrada. Las tecnologías utilizadas suelen ser navegadores web, HTML, CSS, JavaScript y aplicaciones cliente.

#### Nivel 2: Capa de Aplicación o Negocio (Application Tier)

Contiene las reglas de negocio y la lógica que procesa las solicitudes de los usuarios. Actúa como intermediario entre la interfaz y la base de datos. Comúnmente utiliza tecnologías como ASP.NET Core, Java Spring o Node.js.

#### Nivel 3: Capa de Datos (Data Tier)

Se encarga del almacenamiento, consulta y administración de la información persistente. Generalmente utiliza sistemas gestores de bases de datos como SQL Server, PostgreSQL o MySQL.

### Seguridad Perimetral

Exponer directamente una base de datos a Internet constituye una práctica insegura porque aumenta la superficie de ataque del sistema. Un atacante podría intentar acceder a la información mediante ataques de fuerza bruta, explotación de vulnerabilidades o robo de credenciales.

La buena práctica consiste en mantener la base de datos dentro de una red privada y permitir el acceso únicamente a través de la capa de aplicación, utilizando además mecanismos de autenticación, autorización y cifrado de comunicaciones.

---

## 2. Desacoplamiento Lógico con el Patrón MVC

### La Crisis del Código Espagueti

Cuando las consultas SQL, la lógica de negocio y los elementos visuales se encuentran mezclados dentro de un mismo archivo, el software se vuelve difícil de mantener, comprender y extender. Además, las pruebas unitarias se complican debido a que los componentes no pueden evaluarse de forma independiente.

### Separación de Preocupaciones (SoC)

#### Modelo (Model)

Representa los datos y las reglas de negocio de la aplicación. Su responsabilidad consiste en almacenar y manipular información. El modelo no debe conocer detalles relacionados con la interfaz gráfica ni la forma en que los datos son mostrados al usuario.

#### Vista (View)

Es el componente encargado de presentar la información al usuario. Se considera una entidad pasiva porque únicamente muestra los datos recibidos. No debe contener lógica de negocio ni consultas a bases de datos.

#### Controlador (Controller)

Actúa como intermediario entre el modelo y la vista. Recibe las solicitudes del usuario, coordina las operaciones necesarias y selecciona la vista apropiada para responder a la petición.

### Métricas de Ingeniería de Software

El patrón MVC favorece una alta cohesión porque cada componente posee una responsabilidad claramente definida. Asimismo, promueve un bajo acoplamiento debido a que los componentes interactúan mediante interfaces bien establecidas y pueden modificarse sin afectar significativamente a los demás elementos del sistema.

---

# Parte 2: Modelado del Ciclo de Vida y Enrutamiento Semántico

## 1. Mapeo Analítico de URLs

Tomando como base la plantilla:

```text
{controller=Home}/{action=Index}/{id?}
```

se obtiene el siguiente mapeo:

| URL Entrante                                                 | Controlador                | Acción    | id       |
| ------------------------------------------------------------ | -------------------------- | --------- | -------- |
| https://ingenieria.usac.edu.gt/ControlAcademico/Login        | ControlAcademicoController | Login     | Ninguno  |
| https://ingenieria.usac.edu.gt/Estudiante/Historial/20260123 | EstudianteController       | Historial | 20260123 |
| https://ingenieria.usac.edu.gt/Asignacion/Detalle/10         | AsignacionController       | Detalle   | 10       |
| https://ingenieria.usac.edu.gt/Home                          | HomeController             | Index     | Ninguno  |

## 2. Diagramación del Flujo Interactivo

### Paso 1

El usuario realiza una acción en el navegador web, como presionar un botón o acceder a una URL.

### Paso 2

La solicitud HTTP es enviada al servidor ASP.NET Core, donde el sistema de enrutamiento analiza la URL para determinar el controlador y la acción correspondientes.

### Paso 3

El controlador recibe la petición y procesa la solicitud. Si es necesario obtener información, se comunica con el modelo.

### Paso 4

El modelo recupera o procesa los datos requeridos y devuelve el resultado al controlador.

### Paso 5

El controlador envía los datos a la vista. La vista genera el código HTML dinámicamente y el navegador renderiza la respuesta para el usuario.

---

# Parte 4: Auditoría y Control de Calidad

## Prueba de Cohesión (GET)

La acción `Listar()` devuelve directamente la colección de estudiantes hacia la vista correspondiente. El controlador únicamente despacha información y no contiene consultas SQL ni lógica de negocio compleja, cumpliendo con los principios de alta cohesión.

## Evaluación de Antipatrones

Se verificó que ninguno de los métodos del controlador supera las veinte líneas de código. Esto evita la aparición del antipatrón conocido como **Fat Controller**, manteniendo una correcta separación de responsabilidades y facilitando el mantenimiento del sistema.

---

# Conclusiones

1. La arquitectura Multi-Nivel permite distribuir responsabilidades entre diferentes componentes físicos, mejorando la escalabilidad, seguridad y mantenibilidad de los sistemas modernos.

2. El patrón MVC facilita la separación de responsabilidades dentro del software, promoviendo un diseño organizado y reduciendo el acoplamiento entre componentes.

3. La implementación práctica demostró cómo ASP.NET Core MVC integra modelos, vistas y controladores para construir aplicaciones web estructuradas, mantenibles y alineadas con las buenas prácticas de la ingeniería de software.

---

# Referencias Bibliográficas

Facultad de Ingeniería, USAC. (2026). *Sesión 11: Modelado Base y Arquitecturas de Despliegue. Evolución de Sistemas Distribuidos, Fundamentos del Modelo Cliente-Servidor y Diseño Físico Multi-Capas (N-Tier).* Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.

Facultad de Ingeniería, USAC. (2026). *Sesión 12: Arquitectura y Componentes del Patrón MVC. Desacoplamiento Lógico de Software, Ciclo de Vida de las Peticiones y Enrutamiento en Aplicaciones Interactivas Modernas.* Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.
