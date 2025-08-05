# 🗂️ multimedia
Este proyecto define la estructura de la base de datos en MongoDB para la aplicación web **"Mis Recursos App"**, orientada a permitir a los usuarios llevar un registro personalizado de series, películas y libros.

---

## 🧱 Modelo de Base de Datos

La base de datos está compuesta por dos colecciones principales:

---

### 1. 🧍 Colección: `usuarios`

Contiene los datos personales básicos de cada usuario.

#### 📌 Estructura de documento:

```json
{
  "_id": ObjectId,
  "nombre": String,
  "email": String
}
```

- `_id`: Identificador único generado automáticamente por MongoDB.  
- `nombre`: Nombre completo del usuario.  
- `email`: Correo electrónico del usuario.

---

### 2. 🎬 Colección: `recursos`

Almacena los recursos agregados por los usuarios, como libros, series y películas, junto con su estado y apreciaciones personales.

#### 📌 Estructura de documento:

```json
{
  "_id": ObjectId,
  "nombre_recurso": String,
  "genero": String,
  "formato": String,           // "pelicula", "serie", "libro"
  "plataforma": String,
  "estado": String,            // "pendiente", "viendo", "finalizada"
  "fecha_terminacion": Date,   // opcional
  "valoracion": Number,        // 1 a 5, solo si finalizada
  "reseña": String,            // opcional, solo si finalizada
  "id_usuario": ObjectId       // Referencia al _id en la colección usuarios
}
```

🔸 Si el estado del recurso es `"pendiente"` o `"viendo"`, no se debe registrar `valoracion` ni `reseña`.  
🔸 `id_usuario` actúa como referencia para identificar qué usuario registró el recurso.

---

## 🔗 Relación entre colecciones

**Relación uno a muchos**:

- Un usuario (`usuarios`) puede tener muchos recursos (`recursos`), mediante el campo `id_usuario`.

Se optó por este diseño **referenciado** para mantener independencia entre usuarios y sus recursos, facilitando escalabilidad y consultas eficientes.

---

## 🧪 Archivos JSON de prueba

- `usuarios.json`: contiene registros de usuarios de ejemplo.  
- `recursos.json`: contiene registros de libros, películas y series enlazados a usuarios existentes.

---


## 📌 Justificación del Modelo

Se utilizó un enfoque **basado en documentos referenciados** con `ObjectId` para el campo `id_usuario` porque:

- Permite una estructura limpia y escalable.
- Evita duplicación de datos del usuario en cada recurso.
- Facilita futuras operaciones como filtros por usuario o agregaciones.

---
### Atores
Michel rodriguez