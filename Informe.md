# Taller 3 BD
* Jose Grisales
* David Álvarez
## Parte 1
### Esquema propuesto

En MongoDB se crearon dos colecciones principales:

- `comentarios_bares`
- `eventos`

La entidad `Bar` no se duplica completamente en MongoDB. En su lugar, los documentos de comentarios y eventos guardan el campo `bar_id`, que funciona como referencia al identificador del bar almacenado en Oracle.

---

## Diagrama de modelado documental

```
                ┌───────────────────────┐
                │        BARES          │
                │───────────────────────│
                │ ID                    │
                │ NOMBRE                │
                │ CIUDAD                │
                │ PRESUPUESTO           │
                │ CANT_SEDES            │
                └───────────┬───────────┘
                            │
                            │ Referencia: bar_id
                            │ No se embebe el objeto Bar
                            │
        ┌───────────────────┴────────────────────────┐
        │                                            │
        ▼                                            ▼
┌─────────────────────────────┐        ┌─────────────────────────────┐
│     comentarios_bares       │        │          eventos            │
│─────────────────────────────│        │─────────────────────────────│
│ _id                         │        │ _id                         │
│ bar_id  ← referencia        │        │ bar_id  ← referencia        │
│ autor   ← embebido          │        │ nombre  ← embebido          │
│ texto   ← embebido          │        │ fecha_creacion ← embebido   │
│ date    ← embebido          │        │ campos variables embebidos  │
└─────────────────────────────┘        └─────────────────────────────┘
```

La colección `comentarios_bares` almacena los comentarios que los usuarios hacen sobre un bar. Cada comentario es un documento independiente que contiene el identificador del bar, el autor, el texto del comentario y la fecha de creación.

Ejemplo de documento en la colección comentarios_bares:

```
{
  "bar_id": 1,
  "autor": "DAVID",
  "texto": "Muy buen ambiente y buena música.",
  "date": "2026-05-14T10:00:00"
}
```

La colección eventos almacena los eventos anunciados por los bares. Cada evento también es un documento independiente y referencia al bar mediante bar_id.

Ejemplo de evento tipo concierto:
```
{
  "bar_id": 2,
  "nombre": "Noche de Jazz",
  "artista": "Trío Bogotá",
  "cover": 15000,
  "cupos": 80
}
```
* La relación entre `Bar` y `comentarios_bares` se modeló como una **referencia** mediante el campo `bar_id`.
* La relación entre `Bar` y `eventos` también se modeló como una **referencia** mediante el campo `bar_id`. Cada evento pertenece a un bar específico, pero el evento se guarda como un documento independiente en MongoDB.

* Los datos propios de cada comentario se modelaron como campos **embebidos** dentro del mismo documento de comentario. Por ejemplo, `autor`, `texto` y `date` hacen parte directamente del documento en la colección `comentarios_bares`.

* Los datos propios de cada evento se modelaron como campos **embebidos** dentro del documento de evento. Por ejemplo, `nombre`, `artista`, `cover`, `cupos`, `descuento`, `hora_inicio` o `hora_fin` se almacenan directamente dentro del documento en la colección `eventos`.

## API en python
![Post comentarios](imgs\post%20comentarios.png)

![Get comentarios](imgs\get%20comentarios.png)

![Post eventos](imgs\post%20eventos.png)

![Get eventos](imgs\get%20eventos.png)
