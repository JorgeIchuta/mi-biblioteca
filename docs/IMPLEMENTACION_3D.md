# Guía de Implementación: Estante 3D

## 1. Estructura de Datos

### Modelo Actual (1 libro por celda)
```javascript
books = {
  "0:1": { title: "Don Quijote", author: "Cervantes", genre: "Ficción" }
}
```

### Nuevo Modelo (pila de libros por posición)
```javascript
books = {
  "A1": [
    { id: 1, title: "Don Quijote", author: "Cervantes", genre: "Ficción", addedAt: "2024-01-01" },
    { id: 2, title: "1984", author: "Orwell", genre: "Ficción", addedAt: "2024-01-02" }
  ],
  "A2": [...],
  "A3": [...],
  "B1": [...],
  "B2": [...],
  "B3": [...]
}
```

---

## 2. UI Propuesta

```
╔═══════════════════════════════════════════╗
║         📚 SISTEMA DE ESTANTERÍA 3D       ║
╠═══════════════════════════════════════════╣
║  TOTAL: 15 libros | 9 posiciones | 75% ocupación ║
╚═══════════════════════════════════════════╝

┌─────────────────────────────────────────────────────┐
│  🏚️ VISTA 3D DEL ESTANTE                           │
├───────────┬───────────┬───────────┐                 │
│    A1     │    A2     │    A3     │  ← Fila A      │
│  📚 (3)   │  📚 (2)   │  📚 (0)   │    (arriba)    │
├───────────┼───────────┼───────────┤                 │
│    B1     │    B2     │    B3     │  ← Fila B      │
│  📚 (1)   │  📚 (5)   │  📚 (4)   │    (abajo)    │
└───────────┴───────────┴───────────┘                 │
                                                      │
┌─────────────────────────────────────────────────────┐
│  📖 PANEL DE LIBROS [A1] (3 libros)                │
├──────────────────────────────────────────────────────┤
│  [1] Don Quijote    - Cervantes  - Ficción  [👁][✏][🗑]│
│  [2] 1984           - Orwell     - Ficción  [👁][✏][🗑]│
│  [3] La Odisea      - Homero     - Historia [👁][✏][🗑]│
├──────────────────────────────────────────────────────┤
│  [<] [1/3] [>]  ← Navegar pila                     │
└─────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────┐
│  ➕ AGREGAR LIBRO                                   │
├──────────────────────────────────────────────────────┤
│ Título: [________________]  Autor: [________________]│
│ Género: [Ficción ▾]  Posición: [A1 ▾]  [Agregar]   │
└─────────────────────────────────────────────────────┘
```

---

## 3. Funcionalidades

### Core
1. **9 posiciones fijas**: A1, A2, A3, B1, B2, B3
2. **Pila infinita**: Múltiples libros por posición
3. **Navegación**: Ver libro frontal, central, fondo
4. **CRUD completo**: Agregar, editar, ver, eliminar
5. **Persistencia**: localStorage

### UI
6. **Vista 3D del estante**: Render visual de las 6 celdas
7. **Indicador de cantidad**: "(3)" = 3 libros en esa posición
8. **Selector de libro activo**: [<] [2/3] [>]
9. **Panel de información**: Muestra libro seleccionado
10. **Filtros**: Por género, autor, posición

### Extras
11. **Buscar**: Por título, autor o género
12. **Exportar/Importar**: Backup JSON
13. **Estadísticas**: Total libros, por género, por posición
14. **Tema oscuro**: Toggle

---

## 4. Clases/Funciones Necesarias

```javascript
// Constantes
const POSITIONS = ['A1', 'A2', 'A3', 'B1', 'B2', 'B3'];
const GENRES = ['Ficción', 'Ciencia', 'Historia', 'Poesía', 'Infantil', 'Técnico', 'Otro'];

// Datos
let books = {};           // { "A1": [libro1, libro2], "A2": [...] }
let selectedPosition = "A1";  // Posición seleccionada
let currentBookIndex = 0;     // Índice en la pila de la posición

// Funciones principales
init()                       // Inicializar datos
saveData()                   // Guardar en localStorage
renderShelf()                // Renderizar estante 3D
renderBooksList()            // Renderizar panel de libros
addBook(titulo, autor, genero, posicion)
editBook(posicion, index, nuevosDatos)
deleteBook(posicion, index)
selectPosition(pos)
navigatePila(direction)      // +1 o -1 en la pila
filterBooks(filtros)
searchBooks(query)
exportData()
importData(file)
```

---

## 5. Pasos de Implementación

### Paso 1: Estructura HTML
- Contenedor principal
- Header con estadísticas
- Grid del estante (2×3)
- Panel de libros
- Formulario de agregar/editar

### Paso 2: Estilos CSS
- Grid para las 6 celdas del estante
- Estilos para celda vacía vs con libros
- Indicador visual de cantidad
- Panel lateral con lista de libros
- Botones de navegación (< >)
- Tema oscuro

### Paso 3: JavaScript - Datos
- Inicializar estructura `{ "A1": [], "A2": [], ... }`
- Cargar desde localStorage
- Funciones de guardado

### Paso 4: JavaScript - Render
- `renderShelf()`: Dibuja las 6 celdas
- Cada celda muestra posición + cantidad
- Click en celda → selecciona posición

### Paso 5: JavaScript - Lógica
- `addBook()`: Agrega al final de la pila
- `selectPosition()`: Cambia posición activa
- `navigatePila()`: Mueve entre libros de la pila
- `deleteBook()`: Elimina libro específico

### Paso 6: Búsqueda y Filtros
- Input de búsqueda
- Selectores de filtro
- Actualizar vista según resultados

### Paso 7: Extras
- Exportar/Importar JSON
- Tema oscuro
- Validaciones

---

## 6. Ejemplo de Código Inicial

```html
<!-- Estructura básica del estante -->
<div class="shelf">
  <div class="shelf-row">
    <div class="shelf-cell" data-position="A1" onclick="selectPosition('A1')">
      <span class="pos-label">A1</span>
      <span class="book-count">(3)</span>
    </div>
    <div class="shelf-cell" data-position="A2">...</div>
    <div class="shelf-cell" data-position="A3">...</div>
  </div>
  <div class="shelf-row">
    <div class="shelf-cell" data-position="B1">...</div>
    <div class="shelf-cell" data-position="B2">...</div>
    <div class="shelf-cell" data-position="B3">...</div>
  </div>
</div>
```

```css
.shelf {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 20px;
}

.shelf-row {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.shelf-cell {
  width: 150px;
  height: 120px;
  background: #8B4513; /* Color madera */
  border: 3px solid #5D3A1A;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: transform 0.2s;
}

.shelf-cell:hover {
  transform: scale(1.05);
}

.shelf-cell.selected {
  border-color: #FFD700;
  box-shadow: 0 0 15px rgba(255, 215, 0, 0.5);
}
```

---

## 7. Archivo de Datos Inicial

```json
{
  "A1": [
    { "id": 1, "title": "Don Quijote", "author": "Cervantes", "genre": "Ficción", "addedAt": "2024-01-15" },
    { "id": 2, "title": "Cien Años", "author": "García Márquez", "genre": "Ficción", "addedAt": "2024-01-16" }
  ],
  "A2": [
    { "id": 3, "title": "1984", "author": "Orwell", "genre": "Ficción", "addedAt": "2024-01-17" }
  ],
  "A3": [],
  "B1": [
    { "id": 4, "title": "El Principito", "author": "Saint-Exupéry", "genre": "Infantil", "addedAt": "2024-01-18" },
    { "id": 5, "title": "La Odisea", "author": "Homero", "genre": "Historia", "addedAt": "2024-01-19" }
  ],
  "B2": [],
  "B3": []
}
```

---

## 8. Próximos Pasos

1. ¿Confirmar esta estructura?
2. ¿Empezar implementación paso a paso?
3. ¿Agregar alguna característica extra?

¿Te parece siبدء con el código?