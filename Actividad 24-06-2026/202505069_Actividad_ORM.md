# Actividad Corta de Laboratorio: De ADO.NET Tradicional a la Automatización con EF Core

**Nombre:** Jose Carlos González López

**Carnet:** 202505069

**Curso:** Laboratorio de IPC2 "D"

**Fecha:** 24 de junio de 2026

---

## Parte 1: Diagnóstico Técnico y Brecha de Impedancia

### 1. La Brecha de Impedancia

- Clase Clásica (POCO) -> Mapea a -> Tabla
- Propiedad/Atributo -> Mapea a -> Columna
- Instancia de Objeto -> Mapea a -> Fila (Registro)

### 2. Mitigación de Vulnerabilidades

EF Core previene automáticamente la vulnerabilidad de Inyección SQL mediante el uso de consultas parametrizadas generadas internamente por el ORM. Esto evita que los datos proporcionados por el usuario sean interpretados como parte del código SQL.

En ADO.NET tradicional, esta protección se lograba utilizando parámetros SQL. De esta forma, los valores eran enviados por separado de la instrucción SQL, reduciendo el riesgo de inyección.

### 3. Optimización de Infraestructura

El método AsNoTracking() desactiva el rastreador de cambios (Change Tracker) de Entity Framework Core. Como las entidades obtenidas solo serán leídas y no modificadas, EF Core no necesita almacenar información adicional para detectar cambios.

Esto reduce el consumo de memoria RAM y el trabajo del procesador, permitiendo que el servidor atienda más solicitudes con los mismos recursos. Por ello, su uso en consultas de solo lectura representa una optimización eficiente y un mejor aprovechamiento del hardware compartido de la universidad.

---

## Parte 2: Desafío de Refactorización de Código

### 1. Contexto (DbContext)

```csharp
using Microsoft.EntityFrameworkCore;

public class UnidadAcademicaContext : DbContext
{
    public UnidadAcademicaContext(DbContextOptions<UnidadAcademicaContext> options)
        : base(options)
    {
    }

    public DbSet<Catedratico> Catedraticos { get; set; }
}

public class Catedratico
{
    public int Id { get; set; }
    public string Nombre { get; set; }
}
```

### 2. Consulta LINQ con EF Core

```csharp
using Microsoft.EntityFrameworkCore;

public List<Catedratico> ObtenerCatedraticos(UnidadAcademicaContext _context)
{
    return _context.Catedraticos
        .AsNoTracking()
        .Where(c => c.Nombre.StartsWith("Ing."))
        .ToList();
}
```



---

## Parte 3: Referencias Bibliográficas

- Facultad de Ingeniería, USAC. (2026). *Sesión 17: Conectividad con SQL Server. Acceso Estructurado a Datos mediante C# y ADO.NET*. Laboratorio de Introducción a la Programación y Computación 2. Guatemala.

- Facultad de Ingeniería, USAC. (2026). *Sesión 18: Mapeo de Objetos Relacionales. Persistencia Automatizada con Entity Framework Core*. Laboratorio de Introducción a la Programación y Computación 2. Guatemala.
