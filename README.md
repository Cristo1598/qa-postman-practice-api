# QA Practice - Reqres API (Ejercicio 1)

## 🎯 Objetivo

Práctica de API Testing manual con Postman, cubriendo operaciones CRUD completas (Create, Read, Update, Delete) sobre la API pública [reqres.in](https://reqres.in), incluyendo validación de casos positivos y negativos.

Este ejercicio forma parte de mi proceso de transición profesional hacia QA/Testing, aplicando conceptos de:
- Diseño de casos de prueba (positivos y negativos)
- Validación de status codes HTTP
- Validación de estructura y contenido de respuestas (JSON)
- Manejo de autenticación vía API Key
- Uso de variables de entorno en Postman

## 🛠️ Herramientas

- **Postman** (colección + tests en JavaScript)
- **API pública:** reqres.in (requiere autenticación vía `x-api-key`)

## 📋 Casos de prueba cubiertos

| # | Endpoint | Método | Caso | Resultado esperado |
|---|----------|--------|------|---------------------|
| 1 | `/api/users?page=2` | GET | Listar usuarios | 200 OK + estructura `data` válida |
| 2 | `/api/users/2` | GET | Usuario existente (caso positivo) | 200 OK + id coincide |
| 3 | `/api/users/999` | GET | Usuario inexistente (caso negativo) | 404 Not Found |
| 4 | `/api/users` | POST | Crear usuario | 201 Created + datos coinciden con lo enviado |
| 5 | `/api/users/2` | PUT | Actualizar usuario | 200 OK + campo actualizado correctamente |
| 6 | `/api/users/2` | DELETE | Eliminar usuario | 204 No Content |

## 🔎 Detalle de validaciones (tests automatizados en Postman)

Cada request incluye tests en la pestaña **Scripts → Post-response**, usando `pm.test()` para validar:
- Código de estado HTTP correcto
- Presencia y tipo de campos clave en la respuesta (`data`, `id`, `email`, etc.)
- Que los valores devueltos coincidan con los datos enviados (para POST/PUT)
- Manejo correcto de errores (404 para recursos inexistentes)

## 🔐 Nota sobre autenticación

A partir de 2025, reqres.in requiere un header `x-api-key` en todas las requests. Para evitar exponer credenciales, configuré la key como variable de entorno (`{{api_key}}`) en Postman en lugar de escribirla directamente en cada request. **La colección exportada en este repositorio no incluye mi API key real** — cualquiera que quiera reproducir las pruebas debe generar su propia key gratuita en [app.reqres.in](https://app.reqres.in).

## 📂 Contenido del repositorio

- `QA-Practice-Reqres-API.postman_collection.json` — colección exportada con las 6 requests y sus tests
- `/screenshots` — evidencia visual de ejecución
- Este `README.md`

Estructura sugerida del repositorio
jsonplaceholder-api-practice/
├── README.md
├── collections/
│   └── jsonplaceholder-api.postman_collection.json
└── screenshots/
    ├── 01-get-posts.png
    ├── 02-get-post-valid.png
    ├── 03-get-post-404.png
    ├── 04-post-create-201.png
    ├── 05-put-update-200.png
    └── 06-delete-200.png

## 💡 Aprendizajes

- Diseñar casos de prueba positivos y negativos, no solo el "happy path"
- Detectar y adaptarse a cambios en el comportamiento de una API (en este caso, la exigencia reciente de autenticación en reqres.in)
- Buenas prácticas de seguridad: no exponer credenciales en colecciones compartidas
