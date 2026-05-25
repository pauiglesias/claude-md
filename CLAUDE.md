# [Project Name] - CLAUDE.md

Instrucciones para agentes que trabajen en este repositorio. Este archivo es la fuente de verdad para `AGENTS.md`.

> No modifiques `AGENTS.md` directamente. Es un puntero de solo lectura hacia `CLAUDE.md`; toda actualización de instrucciones va en este archivo.

La documentacion adicional para agentes vive solo en `docs/claude/`. El resto de documentacion del repositorio es para humanos y no debe tratarse como fuente de verdad para instrucciones de agente.



## Reglas de trabajo

- No modifiques `AGENTS.md`; si hay que actualizar instrucciones del proyecto, actualiza este archivo.
- `CHANGELOG.md` solo debe actualizarse bajo peticion explicita. No lo mantengas automaticamente en cada cambio: no es fuente de verdad del proyecto, solo anotaciones que referencian el progreso. Antes de anadir entradas, carga y sigue `docs/claude/changelog-file.md`.



## Uso de Git

> ⛔ **PROHIBIDO hacer commits sin orden explícita del usuario.**
>
> Terminar de implementar código no autoriza para hacer commit. Esperar siempre a que el usuario diga "haz commit" o equivalente antes de ejecutar cualquier `git commit`. Esta restricción no tiene excepciones.
>
> Nunca preguntes al usuario "¿hago commit?" o "¿hacemos commit?" (o preguntas similares) cuando termines tu implementación. **NO** hagas ninguna mención a hacer commits. El usuario te lo pedirá en el momento adecuado sin que tú lo tengas que sugerir o preguntar.
>
- No uses Git para buscar en versiones anteriores, historial, commits, ramas remotas, reflog, blame, bisect o arqueología del repositorio salvo petición explícita del usuario.
- Sí puedes usar comandos de inspección del estado actual como `git status -- .`, `git diff -- .` o `git diff --cached -- .` cuando sea necesario para proteger cambios existentes, revisar el trabajo en curso o responder a una petición de revisión. El sufijo `-- .` es obligatorio en todos los comandos de lectura para restringir el alcance al directorio de trabajo primario, incluso cuando la raíz `.git` está en un directorio superior.
- Usa siempre `git -C <directorio-de-trabajo-primario>` para anclar git al directorio del proyecto, independientemente del CWD actual. El directorio de trabajo primario es el que contiene este `CLAUDE.md`. **Nunca** uses `cd` seguido de `&&` con git.
- No ejecutes comandos de Git que expongan o modifiquen ficheros fuera de este directorio de trabajo.
- Antes de ejecutar cualquier `git commit`, carga y sigue `docs/claude/git.md`.
