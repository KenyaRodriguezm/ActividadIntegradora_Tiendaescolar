# Bocetos de pantallas — Sistema de Reportes

## I. Rol: VENDEDOR

### Pantalla 1 — Filtros del reporte de ventas
```
┌─────────────────────────────────────────────┐
│  Reporte de Ventas                     [ ⚙ │
├─────────────────────────────────────────────┤
│ Rango de fechas                             │
│   Desde [ 2026-01-01 ]  Hasta [ 2026-01-31 ]│
│                                             │
│ Categoría (opcional, multi-selección)       │
│   [ ] Bebidas   [ ] Snacks   [ ] Papelería
    []  Galletas                              │
│                                             │
│ Producto (opcional, multi-selección)        │
│   [ Buscar producto...            ▼ ]       │
│                                             │
│              [ Generar reporte ]            │
└─────────────────────────────────────────────┘
```

### Pantalla 2 — Resultado del reporte de ventas
```
┌─────────────────────────────────────────────┐
│  Reporte de Ventas · 01–31 Ene 2026   [ ⬇ ] │
├─────────────────────────────────────────────┤
│ Resumen                                     │
│   Total vendido:      $12,450.00            │
│   Unidades vendidas:  318                   │
│   Transacciones:      146                   │
├─────────────────────────────────────────────┤
│ Venta rgba(0, 3, 34, 0.27) · 2026-01-05 · |
 Cliente: Mitchelle. pamela                   │
│   • Refresco 600ml   x3   $18.00   $54.00   │
│   • Papas 45g        x2   $15.00   $30.00   │
│   Total venta: $84.00                       │
├─────────────────────────────────────────────┤
│ Venta rgba(17, 0, 34, 0.33) · 2026-01-05 
· Cliente: J. López                           │
│   • Cuaderno 100h    x1   $35.00   $35.00   │
│   Total venta: $35.00                       │
└─────────────────────────────────────────────┘
```

---

## II. Rol: COMPRADOR

### Pantalla 3 — Filtro de compras por fecha
```
┌───────────────────────────────────────────── ┐
│  Mis Compras                                 │
├───────────────────────────────────────────── ┤
│ Rango de fechas                              │
│   Desde [ 2026-01-01 ]  Hasta [ 2026-01-31 ] │
│                                              │
│              [ Buscar compras ]              │
└─────────────────────────────────────────────┘
```

### Pantalla 4 — Lista de compras
```
┌─────────────────────────────────────────────  ┐
│  Mis Compras · 01–31 Ene 2026                 │
├─────────────────────────────────────────────  ┤
│ Compra #1024 · 2026-01-05 · $84.00 · Pagada │
│                              [ Ver ticket ]   │
├─────────────────────────────────────────────  ┤
│ Compra #1031 · 2026-01-12 · $50.00 · Pagada │
│                              [ Ver ticket ]   │
└─────────────────────────────────────────────┘
```

### Pantalla 5 — Ticket de compra (detalle)
```
┌─────────────────────────────────────────────┐
│  Ticket TCK-001024                    [ ⬇ ] │
├─────────────────────────────────────────────┤
│ Fecha de compra: 2026-01-05                 │
│ Cliente: Mitchelle pamela                   │
├─────────────────────────────────────────────┤
│ Producto        Cant.   P.Unit.   Subtotal  │
│ Refresco 600ml    3     $18.00     $54.00   │
│ Papas 45g         2     $15.00     $30.00   │
├─────────────────────────────────────────────┤
│ Método de pago: Tarjeta          $84.00     │
│ Total:                           $84.00    │
└─────────────────────────────────────────────┘
```

---

## Notas de diseño (aplicadas también en los XSD)

-Se incluyen solo los campos necesarios para cada uno de los reportes 
-se arrastran columnas de la BD  que sean requeridos 
-En este caso algunos datos como  `activo`,`stock` no aparecen porque no son relevantes para ventas/compras ya finalizadas 
- Los filtros opcionales (`Categorias`, `Productos`) usan `minOccurs="0"`;
  Algunas de las listas de resultados (ventas, compras, productos de un ticket) usan
  `maxOccurs="unbounded"` con `minOccurs` por defecto = 1** (equivalente
  a `+`, no a `*`), porque un reporte generado siempre debe traer al menos
  un registro — si no hay resultados, no se genera el documento.
