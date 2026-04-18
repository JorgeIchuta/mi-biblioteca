# Documentación del Proyecto: Sistema de Estantería 3D

## 📋 Índice

1. [Descripción General](#descripción-general)
2. [Estructura del Proyecto](#estructura-del-proyecto)
3. [Características](#características)
4. [Estructura de Datos](#estructura-de-datos)
5. [Guía de Uso](#guía-de-uso)
6. [Persistencia de Datos](#persistencia-de-datos)
7. [Límites y Restricciones](#límites-y-restricciones)
8. [Tecnologías Utilizadas](#tecnologías-utilizadas)

---

## 1. Descripción General

**Nombre del Proyecto**: Sistema de Estantería 3D

**Tipo**: Aplicación Web (Single Page Application)

**Resumen**: Sistema de gestión de biblioteca personal que simula un estante físico real donde cada posición puede contener múltiples libros apilados verticalmente, permitiendo una organización más realista y eficiente del espacio.

---

## 2. Estructura del Proyecto

```
progrMusic/
├── sistema_libreria.html   # Aplicación completa (HTML + CSS + JS)
├── docs/
│   ├── IDEAS.md           # Ideas y mejoras propuestas
│   └── IMPLEMENTACION_3D.md  # Guía de implementación 3D
```

---

## 3. Características

### ✅ Core
- **6 posiciones de estante**: A1, A2, A3 (fila superior) y B1, B2, B3 (fila inferior)
- **Pilas de libros**: Cada posición puede contener ilimitados libros
- **Navegación por niveles**: Ver libro frontal, del medio, o fondo de la pila
- **CRUD completo**: Agregar, editar, ver detalles y eliminar libros

### ✅ Gestión de Datos
- **8 géneros disponibles**: Ficción, Ciencia, Historia, Poesía, Infantil, Técnico, Filosofía, Otro
- **Campos por libro**: Título, Autor, Género, Fecha de registro
- **Identificador único**: Cada libro tiene un ID automático

### ✅ UI/UX
- **Vista 3D del estante**: Representación visual de las 6 posiciones
- **Indicador de cantidad**: Muestra cuántos libros hay en cada posición
- **Panel de libros**: Lista todos los libros de la posición seleccionada
- **Navegación en pila**: Botones [<] [1/3] [>] para moverse entre libros
- **Tema oscuro**: Toggle para cambiar entre modo claro/oscuro

### ✅ Funcionalidades Extra
- **Búsqueda**: Por título, autor o género en toda la biblioteca
- **Filtros**: Por género y por posición
- **Estadísticas**: Total de libros, libros por género, ocupación del estante
- **Exportar datos**: Descargar toda la biblioteca como archivo JSON
- **Importar datos**: Cargar biblioteca desde archivo JSON
- **Validaciones**: Verificar campos obligatorios antes de guardar

---

## 4. Estructura de Datos

### Modelo de Datos (JSON)

```json
{
  "A1": [
    {
      "id": 1713465600000,
      "title": "Don Quijote",
      "author": "Miguel de Cervantes",
      "genre": "Ficción",
      "addedAt": "2024-04-18"
    }
  ],
  "A2": [],
  "A3": [],
  "B1": [
    {
      "id": 1713465600001,
      "title": "El Principito",
      "author": "Antoine de Saint-Exupéry",
      "genre": "Infantil",
      "addedAt": "2024-04-18"
    }
  ],
  "B2": [],
  "B3": []
}
```

### Descripción de Campos

| Campo | Tipo | Descripción |
|-------|------|--------------|
| `id` | Number | Identificador único (timestamp) |
| `title` | String | Título del libro |
| `author` | String | Autor del libro |
| `genre` | String | Género literaria |
| `addedAt` | String | Fecha de registro (YYYY-MM-DD) |

---

## 5. Guía de Uso

### 5.1 Vista Principal

Al abrir la aplicación verás:

```
┌─────────────────────────────────────────────────────┐
│  📚 SISTEMA DE ESTANTERÍA 3D          [🌙] [📊]    │
├─────────────────────────────────────────────────────┤
│  Total: 5 | Estanterías: 6 | Ocupación: 83%       │
├─────────────────────────────────────────────────────┤
│                                                     │
│   ┌─────────┬─────────┬─────────┐                │
│   │   A1    │   A2    │   A3    │  ← Fila A      │
│   │  (2)    │  (0)    │  (0)    │                │
│   ├─────────┼─────────┼─────────┤                │
│   │   B1    │   B2    │   B3    │  ← Fila B      │
│   │  (1)    │  (0)    │  (2)    │                │
│   └─────────┴─────────┴─────────┘                │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### 5.2 Agregar un Libro

1. Selecciona una **posición** del estante (A1-B3)
2. Completa el **formulario**:
   - Título (obligatorio)
   - Autor (obligatorio)
   - Género (obligatorio)
3. Haz clic en **"Agregar"**
4. El libro se añade al **final de la pila** de esa posición

### 5.3 Ver un Libro en la Pila

1. Haz **clic en una posición** del estante
2. Usa los botones de navegación `[<] [2/3] [>]` para moverte entre libros
3. El panel mostrará los datos del libro activo

### 5.4 Editar un Libro

1. Navega hasta el libro que quieres editar
2. Haz clic en **"Editar"**
3. Modifica los campos en el formulario
4. Haz clic en **"Actualizar"**

### 5.5 Eliminar un Libro

1. Navega hasta el libro que quieres eliminar
2. Haz clic en **"Eliminar"**
3. Confirma la acción en el diálogo

### 5.6 Buscar Libros

1. Ve a la pestaña **"Buscar"**
2. Escribe título, autor o género
3. Los resultados muestran posición y datos del libro

### 5.7 Exportar/Importar Datos

**Exportar**:
- Ve a la pestaña **"Lista de Libros"**
- Haz clic en **"📤 Exportar JSON"**
- Se descargará un archivo `libreria_backup.json`

**Importar**:
- Ve a la pestaña **"Lista de Libros"**
- Haz clic en **"📥 Importar JSON"**
- Selecciona tu archivo `.json`
- La biblioteca se actualizará

---

## 6. Persistencia de Datos

### Cómo se Guardan los Datos

```
┌─────────────────────────────────────────────────────┐
│                   localStorage                      │
├─────────────────────────────────────────────────────┤
│  Clave: "mi_estante_3d"                            │
│  Valor: {"A1":[...],"A2":[...],"B1":[...],...}     │
└─────────────────────────────────────────────────────┘
```

### Características

| Aspecto | Descripción |
|---------|--------------|
| **Automático** | Los cambios se guardan al instante |
| **Persistente** | Se mantiene al cerrar el navegador |
| **Navegador** | Solo existe en el navegador actual |
| **Limpiar** | Se borra al limpiar caché/datos del navegador |

### Hacer Backup

Para no perder datos:
1. Exporta regularmente a JSON
2. Guarda el archivo en tu PC
3. Si borras datos, puedes importar el JSON

---

## 7. Límites y Restricciones

| Límite | Valor |
|--------|-------|
| **Posiciones del estante** | 6 (A1, A2, A3, B1, B2, B3) |
| **Libros por posición** | Ilimitado |
| **Total libros** | Ilimitado |
| **Campos por libro** | 5 (id, title, author, genre, addedAt) |

### Restricciones

- Solo funciona en un navegador a la vez
- No sincroniza entre dispositivos
- Si cambias de navegador, no ves los datos
- Los datos se borran si limpias la caché

---

## 8. Tecnologías Utilizadas

| Tecnología | Versión | Uso |
|------------|---------|-----|
| HTML5 | - | Estructura |
| CSS3 | - | Estilos y diseño responsivo |
| JavaScript (ES6+) | - | Lógica y manipulación del DOM |
| localStorage API | - | Persistencia de datos |

---

## 📌 Notas de Desarrollo

- **Sin dependencias**: No requiere librerías externas
- **Archivo único**: Todo el código está en un solo HTML
- **Compatibilidad**: Funciona en Chrome, Firefox, Edge, Safari
- **Responsivo**: Se adapta a pantallas de escritorio y móviles

---

## 🚀 Futuras Mejoras

Posibles características a agregar:
- [ ] Autenticación de usuarios
- [ ] Base de datos en la nube (Firebase)
- [ ] Código QR por libro
- [ ] Historial de préstamos
- [ ] Generación de reportes PDF
- [ ] App móvil

---

*Documentación generada el 18/04/2026*