# Software Versioning

## Terminología de bumps

**English:**
- Last digit: "bump the patch version" or "do a patch bump" → 1.0.3 to 1.0.4.
- Middle digit: "bump the minor version" or "do a minor bump" → 1.0.3 to 1.1.0.
- First digit: "bump the major version" or "do a major bump" → 1.0.3 to 2.0.0.

**Español:**
- Último dígito: "sube la versión patch" o "haz un patch bump" → 1.0.3 a 1.0.4.
- Segundo dígito: "sube la versión minor" o "haz un minor bump" → 1.0.3 a 1.1.0.
- Primer dígito: "sube la versión major" o "haz un major bump" → 1.0.3 a 2.0.0.

---

## Semántico (SemVer) — el estándar más usado

Formato: **MAJOR.MINOR.PATCH** → `2.4.1`

| Dígito | Cuándo sube | Ejemplo |
|--------|------------|---------|
| **MAJOR** | Cambio que rompe compatibilidad (*breaking change*) | API que cambia y el código antiguo deja de funcionar |
| **MINOR** | Funcionalidad nueva, compatible hacia atrás | Añades un endpoint nuevo sin tocar los viejos |
| **PATCH** | Bug fix, sin nueva funcionalidad | Corriges un cálculo erróneo |

Regla: cuando sube MAJOR, MINOR y PATCH vuelven a 0. Cuando sube MINOR, PATCH vuelve a 0.

---

## Sufijos comunes

- `1.0.0-alpha` → muy inestable, en desarrollo
- `1.0.0-beta` → funcional pero puede tener bugs
- `1.0.0-rc.1` → *release candidate*, casi listo para producción
- `1.0.0` → versión estable

---

## Casos especiales

- **`0.x.x`** → fase de desarrollo inicial, la API puede cambiar sin avisar
- **`1.0.0`** → el momento en que declaras que tu software es estable y público

---

## Otros esquemas

- **CalVer** — basado en fechas: `2025.05.26` (Ubuntu lo usa: `24.04`)
- **Incremental** — simplemente `v1, v2, v3...` (APIs internas)

---

La referencia oficial es [semver.org](https://semver.org) si alguna vez necesitas los casos edge.
