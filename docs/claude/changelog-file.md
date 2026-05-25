# Instrucciones para mantener CHANGELOG.md

El archivo `CHANGELOG.md` está en la raíz del proyecto. Lee este documento antes de añadir cualquier entrada.

## Formato

El formato sigue [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Las versiones siguen [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Reglas de edición

- Añadir siempre una nueva versión **encima** de la anterior (orden descendente: más reciente primero).
- Cada versión tiene el encabezado `## [X.Y.Z] - YYYY-MM-DD`.
- Las secciones válidas dentro de una versión son: `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security`. Usar solo las que apliquen.
- Las entradas son frases cortas en pasado o infinitivo, en español.
- No incluir detalles de implementación interna ni referencias a commits.

## Cuándo actualizar

Solo bajo petición explícita del usuario. No es una actualización automática ante cambios en el código.
