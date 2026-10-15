# Ciclo de versiones

Protocolo de actuación para desarrollar, cerrar y publicar una versión. **No es un flujo automático**: el agente asiste, propone el siguiente paso y espera la aprobación explícita del usuario antes de ejecutarlo. Ningún paso se da por autorizado por haber terminado el anterior.

Cárgalo al crear una rama de versión, subir la versión, cerrar una release, hacer un hotfix o mergear a `main`. Las reglas de comandos y commits de `git.md` y las de `changelog-file.md` siguen vigentes; este documento las ordena en secuencia y las extiende, solo para el ciclo de versión, con las operaciones git de la sección "Comandos".

## Principios

- **El agente guía el proceso.** Es quien conoce el ciclo: en cada momento indica en qué paso estamos y **propone el siguiente**, incluidos el cierre de versión (changelog, `status.md`), el despliegue, el merge y el tag. El usuario no tiene que recordar el protocolo ni pedir cada paso por su nombre.
- **Un paso, una aprobación.** Proponer no es ejecutar: antes de cada paso numerado, el agente explica qué va a hacer y espera el visto bueno. Si el usuario no lo da, no se avanza. La aprobación de un paso no vale para el siguiente.
- **Commits: la excepción.** Siguen siendo solo bajo petición explícita del usuario (ver `git.md`). Terminar de implementar o de editar docs no autoriza el commit, y el agente no lo sugiere ni lo pregunta; el usuario lo pide cuando quiere. Ese silencio no se extiende a los demás pasos, que sí se proponen.
- **Trailers de atribución** (`Co-Authored-By` y similares) en commits, merges o tags: se rigen por `git.md`.
- **`main` solo contiene lo estable.** El desarrollo, los hotfixes y las pruebas viven en la rama de la versión; a `main` solo llega lo desplegado, probado y aprobado.

## Nomenclatura

- **Rama:** `X.Y.Z-slug`, con el slug en minúsculas, ASCII sin tildes, palabras separadas por guiones y descriptivo (mínimo 2-3 palabras). Ejemplo: `1.0.3-correccion-login`.
- **Intentos alternativos:** si el desarrollo de una rama no convence, se crea otra desde `main` con sufijo numérico: `1.0.3-correccion-login-2`, `-3`, etc. Son alternativas, no ramas paralelas a mergear: solo una llega a `main`. Las descartadas **se conservan** sin borrar.
- **Tag:** `vX.Y.Z`, anotado, sobre el merge commit en `main`.

## Reglas de versión (semver aplicado al proyecto)

| Cambio | Incremento |
|---|---|
| Bugfix | patch (`1.0.2` → `1.0.3`) |
| Mejora o funcionalidad nueva compatible | minor (`1.0.x` → `1.1.0`) |
| Cambio incompatible (API, comportamiento visible roto) | major |
| Solo documentación, specs o CLAUDE.md | **no consume versión** (va directo a `main` o dentro de la rama activa) |

## La spec

- Vive en `docs/spec/`. Puede estar en `main` antes de crear la rama, o nacer ya dentro de la rama de la versión.
- Lleva en cabecera el campo **`Versión objetivo: X.Y.Z`** (y el slug previsto).
- Una spec en `main` es **exploratoria**: no compromete a implementarla ni a esa versión. La versión objetivo es provisional hasta que se crea la rama; si la exploración se descarta o cambia de versión, se actualiza o marca la spec, sin más.
- Al crear la rama, la versión objetivo de la spec y la de la rama deben coincidir.

## Ciclo

1. **Spec** con `Versión objetivo` (en `main` o en la rama). Si es de `main`, solo existe como propuesta.
2. **Crear la rama** `X.Y.Z-slug` desde `main` (o `-2`, `-3` si es un nuevo intento).
3. **Subir la versión** en los archivos de versión del proyecto, dentro de la rama y antes de desarrollar.
4. **Desarrollar y probar.** Los hotfixes durante el ciclo se hacen **en esta misma rama**, no en `main`.
5. **Cerrar la versión**, que el agente propone cuando el desarrollo y las pruebas están terminados y el usuario aprueba: entrada en `CHANGELOG.md` (siguiendo `changelog-file.md`) y actualización de `docs/claude/status.md`.
6. **Despliegue en producción.** El agente no despliega sin aprobación.
7. **Merge a `main`**, que el agente propone solo cuando el usuario confirma que todo está desplegado, correcto y probado, y con su aprobación:
   - `git merge --no-ff X.Y.Z-slug` estando en `main`.
   - Crear el tag anotado `vX.Y.Z` sobre el merge commit.
   - **La rama se conserva.**

## Comandos

Las operaciones de este ciclo (`switch`, `merge`, `tag`) no son frecuentes y `git.md` no las contempla: este documento las autoriza de forma explícita, solo dentro del ciclo y en el paso correspondiente, con la aprobación del usuario. Cualquier otra operación git de escritura, como `push`, queda fuera y requiere petición expresa.

Para todo lo demás rigen las reglas de `git.md`: `git -C <directorio-de-trabajo-primario> ...`, sin `cd`, un comando por llamada y mensajes con varios `-m` (nunca heredoc ni `$()`). Las rutas de ficheros, si las hay, siguen la convención del proyecto (absolutas o relativas al directorio de trabajo primario), nunca con `../`. Los comandos de lectura llevan `-- .`.

```sh
git -C <directorio-de-trabajo-primario> switch -c 1.0.3-correccion-login main
git -C <directorio-de-trabajo-primario> switch main
git -C <directorio-de-trabajo-primario> merge --no-ff 1.0.3-correccion-login -m "Merge 1.0.3-correccion-login"
git -C <directorio-de-trabajo-primario> tag -a v1.0.3 -m "v1.0.3"
```

Antes del `switch` a `main`, el `merge` y el `tag`, comprobar que el árbol de **todo el repositorio** está limpio y que la rama a mergear es la elegida, no una alternativa descartada. Si el árbol no está limpio, no se ejecuta ninguna de las tres operaciones: se informa al usuario y se espera sus instrucciones.

```sh
git -C <directorio-de-trabajo-primario> status
```

> **Excepción explícita a la regla `-- .` de `git.md`:** esta comprobación se ejecuta deliberadamente sin `-- .`, porque `switch`, `merge` y `tag` operan sobre todo el repositorio y cambios pendientes fuera del directorio de trabajo también los afectan. Es el único uso permitido de `git status` sin `-- .`, limitado a decidir si se continúa o se aborta, no a explorar el repositorio.
