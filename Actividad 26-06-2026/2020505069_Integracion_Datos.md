# Actividad de Laboratorio: Interoperabilidad y Carga Masiva de Datos

**Nombre:** Jose Carlos González López

**Curso:** Laboratorio de Introducción a la Programación y Computación 2

**Fecha:** 17 de junio de 2026

## Parte 1: Evaluación Conceptual y Buenas Prácticas

### 1. Formatos de Intercambio

| Formato | Ventajas | Desventajas |
|---------|----------|-------------|
| **CSV** | Formato simple, ligero, fácil de generar y procesar. Ocupa poco espacio y es ideal para grandes volúmenes de datos tabulares. | No soporta estructuras jerárquicas, tipos de datos ni metadatos. Es propenso a errores de formato. |
| **XML** | Permite representar datos complejos y jerárquicos. Es extensible y autodescriptivo. | Es más pesado, ocupa más espacio y su procesamiento es más lento que CSV. |

### 2. Diferenciación de Procesos

**Serialización** es el proceso de convertir un objeto de C# en un formato de intercambio de datos, como JSON, utilizando `System.Text.Json`.

**Deserialización** es el proceso inverso: consiste en convertir un documento JSON nuevamente en un objeto de C#, utilizando métodos como `JsonSerializer.Deserialize<T>()`.

### 3. El Antipatrón del Rendimiento (N+1)

El problema **N+1** ocurre cuando por cada registro leído de un archivo se realiza una operación individual hacia la base de datos, provocando un gran número de consultas o inserciones y reduciendo considerablemente el rendimiento.

La estrategia recomendada es el **Batching**, que consiste en almacenar temporalmente los registros en una colección y realizar una única inserción masiva mediante `AddRange()` seguida de una sola llamada a `SaveChangesAsync()`.

---

# Parte 2: Implementación Práctica en C#

## Desafío 1: Consumo de Endpoints y Deserialización

```csharp
using System.Text.Json;

public async Task<List<Alumno>?> ObtenerAlumnosAsync()
{
    using HttpClient client = new HttpClient();

    try
    {
        HttpResponseMessage response = await client.GetAsync("https://api.usac.edu/v1/alumnos");

        response.EnsureSuccessStatusCode();

        string json = await response.Content.ReadAsStringAsync();

        JsonSerializerOptions options = new JsonSerializerOptions
        {
            PropertyNameCaseInsensitive = true
        };

        return JsonSerializer.Deserialize<List<Alumno>>(json, options);
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
        return null;
    }
}
```

---

## Desafío 2: Endpoint para Carga Masiva CSV

```csharp
using Microsoft.AspNetCore.Mvc;

[HttpPost]
public async Task<IActionResult> CargarCsv(IFormFile archivo)
{
    if (archivo == null || archivo.Length == 0)
    {
        return BadRequest("Archivo inválido.");
    }

    List<Alumno> alumnos = new List<Alumno>();

    using (var stream = archivo.OpenReadStream())
    using (var reader = new StreamReader(stream))
    {
        // Omitir encabezado
        await reader.ReadLineAsync();

        string? linea;

        while ((linea = await reader.ReadLineAsync()) != null)
        {
            string[] datos = linea.Split(',');

            Alumno alumno = new Alumno
            {
                Carnet = datos[0],
                Nombre = datos[1],
                Carrera = datos[2]
            };

            alumnos.Add(alumno);
        }
    }

    await _context.Alumnos.AddRangeAsync(alumnos);
    await _context.SaveChangesAsync();

    return Ok("Carga masiva realizada correctamente.");
}
```

---

# Parte 3: Referencias Bibliográficas

Facultad de Ingeniería, USAC. (2026). *Sesión 20: Integración de Datos. Consumo de APIs Externas y Carga Masiva (CSV/XML).* Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.
