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
<img width="1102" height="729" alt="get eventos" src="https://github.com/user-attachments/assets/104c0a26-4c5a-4cdd-b0fb-1a845c58e9af" />

<img width="1097" height="940" alt="post eventos" src="https://github.com/user-attachments/assets/7bcd55ca-63ee-4f97-8083-addc428c2be8" />

<img width="1121" height="795" alt="get comentarios" src="https://github.com/user-attachments/assets/6fd484e6-eac2-48ff-b822-b0e3c2357324" />

<img width="1096" height="925" alt="post comentarios" src="https://github.com/user-attachments/assets/154d64fa-c912-4660-916c-fbeb521879cc" />

## Render
https://taller-3-bd-x06p.onrender.com
## Implementacion Comentarios en APEX
<img width="952" height="951" alt="Captura de pantalla 2026-05-14 203003" src="https://github.com/user-attachments/assets/b7a617f1-2bea-4731-b63f-281cdbf3c7bf" />
<img width="948" height="951" alt="Captura de pantalla 2026-05-14 203012" src="https://github.com/user-attachments/assets/3548d59e-089d-46f2-985d-61dca3a81714" />
<img width="954" height="947" alt="Captura de pantalla 2026-05-14 203054" src="https://github.com/user-attachments/assets/0a97bdc1-19e5-4900-aa0e-3913051da300" />
<img width="1122" height="743" alt="Captura de pantalla 2026-05-14 203111" src="https://github.com/user-attachments/assets/522d474d-fe40-473c-a44d-2c53b3015a52" />

## Parte 3 evidencias
<img width="1918" height="951" alt="image" src="https://github.com/user-attachments/assets/af7d9581-29e1-4fa7-9b6b-6e15d890e3ba" />


