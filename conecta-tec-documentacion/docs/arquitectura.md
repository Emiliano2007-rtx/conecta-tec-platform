# Conecta Tec — Arquitectura

> **Estado:** documentación del avance identificado en la evidencia disponible. No se presentan como terminadas las capas o funciones que aún no han sido comprobadas.

## 1. Descripción general

Conecta Tec es una plataforma web para la comunidad del Instituto Tecnológico de Ocotlán. El backend está desarrollado con Java y Spring Boot y expone una API REST. La persistencia utiliza PostgreSQL.

## 2. Tecnologías identificadas

- Java
- Spring Boot
- PostgreSQL
- Bruno para pruebas HTTP
- DBeaver para administrar la base de datos

El proyecto utiliza SQL mediante `JdbcTemplate` como enfoque de acceso a datos, de acuerdo con la arquitectura planteada para el backend.

## 3. Organización por responsabilidades

| Componente | Responsabilidad |
|---|---|
| Controller | Recibe las solicitudes HTTP y devuelve respuestas. |
| Service | Coordina la lógica de la aplicación y las validaciones. |
| Repository | Ejecuta operaciones de acceso a datos. |
| Model | Representa los datos utilizados por la aplicación. |
| DTO | Define los datos que la API recibe o devuelve, cuando se implementen. |

## 4. Flujo general

```text
Cliente (frontend o Bruno)
          |
          | HTTP / JSON o formulario
          v
      Controller
          |
          v
       Service
          |
          v
      Repository
          |
          | SQL
          v
      PostgreSQL
```

1. El cliente envía una solicitud HTTP.
2. El Controller recibe la solicitud.
3. El Controller delega la operación al Service.
4. El Service coordina la operación y solicita datos al Repository cuando corresponde.
5. El resultado regresa al Controller para generar la respuesta HTTP.

> Este diagrama representa la separación de responsabilidades prevista.

## 5. Funcionalidad identificada

El controlador de usuarios utiliza la ruta base `/api/usuarios`. Las rutas que aparecen en la evidencia se documentan en `endpoints.md`.

## 6. Base de datos

La aplicación utiliza PostgreSQL. La base identificada en DBeaver se llama `conecta-tec-db`. Sus tablas y relaciones se documentan por separado en `base-de-datos.md`.

## 7. Estado del proyecto

### Identificado en la evidencia

- API de usuarios con consulta, registro e inicio de sesión.
- Pruebas manuales de solicitudes HTTP mediante Bruno.
- Base de datos PostgreSQL `conecta-tec-db`.
- Tablas para usuarios, publicaciones, archivos, moderaciones, reacciones y reportes.

### Por completar o verificar

- Documentar con evidencia las capas Service y Repository.
- Verificar y documentar las operaciones PUT y DELETE si siguen implementadas.
- Completar pruebas de validaciones y respuestas de error.
- Integrar el frontend con el backend.
- Definir y documentar los DTO de entrada y salida que se utilicen.

## 8. Seguridad

Las respuestas de la API deben incluir únicamente los datos necesarios para el cliente. No se deben exponer contraseñas ni hashes de contraseñas. Las credenciales de PostgreSQL deben mantenerse fuera del repositorio.

## 9. Evidencias

El código fuente del proyecto es privado, por lo que este documento no incluye capturas del código. Las evidencias del funcionamiento de la API están en `endpoints.md` y las de la base de datos en `base-de-datos.md`.
