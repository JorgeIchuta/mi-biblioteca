# Sistema de Inventario para Libros

## 🎯 Contexto

- **Cantidad de posiciones**: 6 (A1, A2, A3, B1, B2, B3)
- **Total de libros**: ~60 títulos
- **Precios**: 6bs a 15bs (rango)
- **Problema**: Ordenar para encontrar libros fácil

---

## 📊 Distribución Actual

```
60 libros ÷ 6 posiciones = 10 libros por posición (promedio)

Esto es mucho, por eso usaremos grupos de precio por posición
```

---

## 💡 Solución: Agrupar por Precio en cada Posición

**Ejemplo de distribución:**

```
POSICIÓN A1 (10 libros - Precio: 6bs-8bs)
├─ Libro 1 - 7bs
├─ Libro 2 - 6bs
├─ Libro 3 - 8bs
└─ ...

POSICIÓN A2 (10 libros - Precio: 9bs-10bs)
├─ Libro 1 - 9bs
├─ Libro 2 - 10bs
└─ ...

POSICIÓN A3 (10 libros - Precio: 11bs-12bs)
...

POSICIÓN B1 (10 libros - Precio: 13bs-14bs)
...

POSICIÓN B2 (10 libros - Precio: 15bs)
...

POSICIÓN B3 (10 libros - Precio: varios)
```

---

## 📋 Campos del Libro

| Campo | Descripción | Ejemplo |
|-------|-------------|---------|
| 📖 Título | Nombre del libro | "Lenguaje 1°" |
| ✍️ Editorial | Casa editorial | "Santillana" |
| 💰 Precio | Precio en bs | 10 |
| 📦 Stock | Cantidad de copias | 3 |
| 📍 Ubicación | Posición | A1 |

---

## 🎯 Vista de la Aplicación

```
┌─────────────────────────────────────────────────────────────┐
│ 🔍 [Buscar libro por título...]         [+ Nuevo] [🌙]     │
├─────────────────────────────────────────────────────────────┤
│  FILTROS:                                                   │
│  Precio: [Todos ▼] [6-8bs] [9-10bs] [11-12bs] [13-15bs]  │
├─────────────────────────────────────────────────────────────┤
│  📊 Total: 60 títulos | Stock: 150 copias                 │
├─────────────────────────────────────────────────────────────┤
│  # │ Título                  │ Editorial  │ Precio │ Stock │
│  1 │ Lenguaje 1° Pri        │ Santillana │  7 bs  │   5   │
│  2 │ Lectura 2° Pri         │ Norma      │  8 bs  │   3   │
│  3 │ Comunicación 3° Sec    │ Santillana │  10 bs │   4   │
│  4 │ Ortografía 1° Pri      │ McGraw     │  6 bs  │   6   │
│  ...                                                      │
├─────────────────────────────────────────────────────────────┤
│  📍 VER ESTANTE:                                            │
│  ┌────┬────┬────┐                                         │
│  │ A1 │ A2 │ A3 │  → 6bs-12bs                             │
│  ├────┼────┼────┤                                         │
│  │ B1 │ B2 │ B3 │  → 12bs-15bs                            │
│  └────┴────┴┘                                            │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗂️ Sistema de Ubicación

```
┌─────────────────────────────────────────┐
│           ESTANTE (6 posiciones)        │
├─────────┬─────────┬─────────┬───────────┤
│    A1   │    A2   │    A3   │  ← Fila A  │
│ 6-8 bs  │ 8-10 bs │ 10-12 bs│           │
├─────────┼─────────┼─────────┼───────────┤
│    B1   │    B2   │    B3   │  ← Fila B  │
│ 12-13 bs│ 13-14 bs│ 14-15 bs│           │
└─────────┴─────────┴─────────┴───────────┘

* Al agregar libro, seleccionas la posición según el precio
```

---

## 📈 Resumen de Precios

| Rango de Precio | Cantidad de Títulos |
|----------------|---------------------|
| 6-8 bs | ~15 |
| 8-10 bs | ~15 |
| 10-12 bs | ~15 |
| 12-15 bs | ~15 |

---

## ✅ LISTO PARA IMPLEMENTAR

**El sistema tendrá:**
- ✅ Buscador por título
- ✅ Filtros por rango de precio
- ✅ 6 posiciones (A1-B3)
- ✅ CRUD de libros (agregar, editar, eliminar)
- ✅ Stock por libro
- ✅ Vista del estante
- ✅ Exportar/Importar JSON
- ✅ Modo oscuro
- ✅ Persistencia de datos

---

*¿Empiezo a implementar?*