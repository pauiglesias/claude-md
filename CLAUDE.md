# [Project Name] - CLAUDE.md

Instrucciones para agentes que trabajen en este repositorio. Este archivo es la fuente de verdad para `AGENTS.md`.

> No modifiques `AGENTS.md` directamente. Es un puntero de solo lectura hacia `CLAUDE.md`; toda actualización de instrucciones va en este archivo CLAUDE.md.

La documentacion adicional para agentes vive solo en `docs/claude/`. El resto de documentacion del repositorio es para humanos y no debe tratarse como fuente de verdad para instrucciones de agente.



## Reglas de trabajo

- Escribe las instrucciones de CLAUDE.md en Español de España, excepto la nomenclatura técnica en su lenguaje de origen.
- **NUNCA** navegar, buscar ni leer archivos fuera del directorio raíz del proyecto (donde reside este `CLAUDE.md`).
- Todas las herramientas de búsqueda y exploración (Glob, Grep, Read, etc.) deben limitarse a la carpeta del proyecto.
- Respetar el archivo `.claudeignore`: no acceder nunca a los archivos o directorios listados en él.
- `CHANGELOG.md` solo debe actualizarse bajo peticion explicita. No lo mantengas automaticamente en cada cambio: no es fuente de verdad del proyecto, solo anotaciones que referencian el progreso. Antes de anadir entradas, carga y sigue `docs/claude/changelog-file.md`.



## Descripción del proyecto

@todo



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




## Estilo de código JavaScript

### Variables
- Usa `const` por defecto, `let` cuando se necesita reasignación. Nunca uses `var`.

### Bloques de control
- **Nunca** escribir sentencias de una sola línea sin llaves. Siempre abrir bloque con `{`, salto de línea, cuerpo y `}`:
```js
// Mal
if (!value) return true;

// Bien
if (!value) {
	return true;
}
```
- Después de cerrar un bloque con llaves hacer un salto de línea extra, a excepción de encontrarnos al final de la función o del archivo.



## Estilos CSS con distribución jerárquica

- Los estilos de administración se definen en `[main css assets file]`, evitando estilos inline.
- Usar jerarquías CSS representadas por **indentación con espacios** (4 espacios por nivel) para selectores anidados:
```css
.dbi-dashboard-top {
    margin-bottom: 15px;
}

    .dbi-views-panels-menu {
        min-height: 100%;
    }

        .dbi-views-panels-menu ul {
            padding: 0;
            display: flex;
            gap: 25px;
        }
```
