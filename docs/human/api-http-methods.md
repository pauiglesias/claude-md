# Métodos HTTP en la API REST

Resumen de qué hace cada método HTTP y cómo se usa en la API del SGA
(`/api/v1/`). Especificación completa en `docs/spec/rest-api.md`.

## Resumen

| Método | Qué hace | Ejemplo en esta API |
|---|---|---|
| `GET` | Leer, sin cambiar nada | `GET /api/v1/trabajadores/` lista, `GET /api/v1/trabajadores/5/` da el detalle |
| `POST` | Crear un recurso nuevo | `POST /api/v1/trabajadores/` da de alta un trabajador |
| `PUT` | Modificar un recurso existente enviándolo **entero** | `PUT /api/v1/trabajadores/5/` con todos los campos |
| `PATCH` | Modificar solo **algunos campos** de un recurso existente | `PATCH /api/v1/trabajadores/5/` con `{"is_active": false}` |

`POST` sirve para crear, no para modificar. La modificación va con `PUT` y
`PATCH`.

## `PUT` frente a `PATCH`

- Con `PUT` hay que mandar todos los campos obligatorios, aunque no cambien.
  Los que falten se rechazan con `400`, porque se entiende que se reemplaza el
  recurso completo.
- Con `PATCH` se manda solo lo que cambia y el resto queda igual. En el código
  (`RestUpdateMixin`, `code/rest/viewsets/base.py`) la diferencia es el
  parámetro `partial`.

## En esta API

- `GET` exige `can_read` en el scope de la credencial para el dominio del
  recurso. `POST`, `PUT` y `PATCH` exigen `can_write`.
- `DELETE` no existe en ningún endpoint.
- Partes de confirmación solo admite `POST` (y lectura). `PUT` y `PATCH`
  devuelven `405`.
- Los recursos de solo lectura (bajas no asignadas, partes no asignados y
  catálogos) no admiten ningún método de escritura.
- `api_mode=dev` funciona con los tres métodos de escritura (`POST`, `PUT` y
  `PATCH`): valida y calcula sin guardar nada.
