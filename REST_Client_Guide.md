
# Guía Completa de REST Client en Visual Studio Code

## **Nivel 1: Básico**
Aprendamos los fundamentos y cómo usar REST Client para realizar pruebas simples de APIs.

### **¿Qué es REST Client?**
Es una extensión de VS Code que permite realizar solicitudes HTTP directamente desde un archivo `.rest` o `.http`. 
Puedes enviar `GET`, `POST`, `PUT`, `DELETE`, entre otros, y ver las respuestas en tiempo real.

### **Instalación**
1. Busca "REST Client" en la extensión de VS Code y haz clic en **Instalar**.
2. Verifica que la extensión esté activa.

### **Cómo funciona**
1. Crea un archivo `requests.rest` (o `.http`).
2. Escribe tu solicitud HTTP, por ejemplo:
   ```http
   GET https://jsonplaceholder.typicode.com/posts
   ```

3. Coloca el cursor sobre la línea de la solicitud y haz clic en **"Send Request"** o presiona `Ctrl+Alt+R`.

4. Verás la respuesta en un panel a la derecha.

### **Ejemplo Básico**
```http
# Obtener todos los posts
GET https://jsonplaceholder.typicode.com/posts
```

---

## **Nivel 2: Intermedio**
Aquí aprenderás a usar parámetros, encabezados y variables.

### **Encabezados personalizados**
Puedes agregar encabezados como `Content-Type` o `Authorization`:

```http
# Obtener con encabezados
GET https://jsonplaceholder.typicode.com/posts
Content-Type: application/json
Authorization: Bearer <token_aqui>
```

### **Cuerpo de la solicitud (Request Body)**
Para solicitudes `POST` o `PUT` puedes enviar datos en formato JSON:

```http
# Crear un post
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
  "title": "Nuevo Post",
  "body": "Contenido del post",
  "userId": 1
}
```

### **Uso de variables**
Define variables reutilizables en un archivo `.env` o directamente en tu archivo `.rest`:

```http
@baseUrl = https://jsonplaceholder.typicode.com

# Obtener usando variable
GET {{baseUrl}}/posts/1
```

---

## **Nivel 3: Avanzado**
Aprenderás a manejar flujos complejos, autenticación y depuración.

### **Combinación de múltiples solicitudes**
Usa separadores `###` para ejecutar solicitudes independientes en el mismo archivo:

```http
# Obtener posts
GET {{baseUrl}}/posts

###

# Crear un nuevo post
POST {{baseUrl}}/posts
Content-Type: application/json

{
  "title": "Post Avanzado",
  "body": "Más contenido",
  "userId": 2
}
```

### **Extracción de valores**
Puedes usar valores de una respuesta en otra solicitud:
1. Extrae datos con expresiones regulares:
   ```http
   GET {{baseUrl}}/posts/1
   ```
   Haz clic en **Save Response Body** y selecciona datos que puedes reutilizar manualmente.

2. Integra los datos:
   ```http
   POST {{baseUrl}}/comments
   Content-Type: application/json

   {
     "postId": {{idExtraido}},
     "comment": "Comentario generado desde respuesta"
   }
   ```

### **Testeo avanzado con GraphQL**
REST Client también soporta GraphQL:

```http
POST https://api.spacex.land/graphql/
Content-Type: application/json

{
  "query": "{ launchesPast(limit: 2) { mission_name launch_date_local } }"
}
```

### **Autenticación**
Prueba APIs protegidas con:
- Tokens Bearer:
  ```http
  Authorization: Bearer {{token}}
  ```

- Autenticación básica:
  ```http
  Authorization: Basic {{username:password}}
  ```

---

## **Nivel 4: Tips y Mejores Prácticas**

### **Organización**
1. Divide tus solicitudes en diferentes archivos para mayor claridad (`usuarios.rest`, `posts.rest`).
2. Usa comentarios (`#`) para describir cada solicitud.

### **Uso de Entornos**
Define entornos con diferentes configuraciones (`dev`, `prod`):
```http
@env = dev

@dev.baseUrl = http://localhost:3000
@prod.baseUrl = https://api.miapp.com

GET {{baseUrl}}/endpoint
```

Cambia fácilmente entre entornos ajustando la variable `@env`.

### **Depuración**
1. Usa herramientas como [Mocky](https://mocky.io) para simular respuestas de APIs.
2. Guarda respuestas con:
   ```http
   ### Save Response To: ./response.json
   ```

### **Integración con APIs reales**
Puedes usar APIs públicas como:
- [JSONPlaceholder](https://jsonplaceholder.typicode.com)
- [OpenWeather](https://openweathermap.org/api)
- [Giphy](https://developers.giphy.com)

---

## **Nivel 5: Maestría**

### **Automatización de pruebas**
Integra REST Client con scripts para automatizar pruebas:
1. Define un conjunto de pruebas en un archivo `.rest`.
2. Ejecuta solicitudes automáticamente usando comandos.

### **Documentación Dinámica**
Usa REST Client como un reemplazo ligero de Postman para compartir solicitudes con otros desarrolladores.

1. Comparte archivos `.rest` directamente.
2. Combina con Markdown para crear documentación legible:
   ```markdown
   ## API de Usuarios
   ### Obtener usuarios
   ```http
   GET https://api.miapp.com/users
   ```

### **Atajos de teclado**
- `Ctrl+Alt+R`: Ejecutar solicitud.
- `Ctrl+Alt+L`: Ejecutar todas las solicitudes en el archivo.

---

¡Con esta guía estás listo para manejar REST Client desde lo básico hasta flujos avanzados! 🚀
