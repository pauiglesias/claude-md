# Git

Instrucciones específicas para usar Git en este repositorio bajo petición explícita del usuario.

## Comandos

- Usa siempre `git -C <directorio-de-trabajo-primario>` para anclar git al directorio del proyecto, independientemente del CWD actual. El directorio de trabajo primario es el directorio desde el que se lanzó Claude Code (el que contiene `CLAUDE.md`).
- Añade siempre `-- .` al final de **todos** los comandos de lectura (`status`, `diff`, `log`) para restringir el alcance al directorio de trabajo. Este sufijo es obligatorio incluso cuando `.git` está en un directorio superior al proyecto: sin él, git opera sobre el árbol completo del repositorio y puede exponer o incluir archivos fuera del directorio de trabajo primario.
- Para `git add`, usa siempre rutas de archivo explícitas. Nunca uses `git add .`, `git add -A` ni patrones glob no acotados. Las rutas nunca deben contener `../`: cualquier ruta que suba por encima del directorio de trabajo está prohibida.
- Nunca uses `cd ... && git ...`.
- No uses Git para buscar en versiones anteriores salvo petición explícita.
- No ejecutes comandos de Git que expongan o modifiquen ficheros fuera de este directorio de trabajo.

Ejemplo correcto (sustituyendo `<directorio-de-trabajo-primario>` por la ruta real):

```sh
git -C /path/to/project status -- .
git -C /path/to/project diff -- .
git -C /path/to/project log -- .
git -C /path/to/project add CLAUDE.md docs/claude/git.md
git -C /path/to/project commit -m "Document git usage rules"
```

Ejemplo incorrecto:

```sh
cd /path/to/project && git add CLAUDE.md && git commit -m "mensaje"
git add CLAUDE.md        # sin -C, depende del CWD implícito
git add .                # captura archivos fuera del proyecto
git -C /path/to/project status  # sin -- ., expone todo el repo
git -C /path/to/project log     # sin -- ., muestra commits de todo el repositorio
```

## Commits

- Antes de ejecutar cualquier `git commit`, verifica que el staging area no contiene ficheros fuera del directorio de trabajo. Ejecuta estos dos comandos y compara su output:

  ```sh
  git -C <directorio-de-trabajo-primario> diff --cached --name-only
  git -C <directorio-de-trabajo-primario> diff --cached --name-only -- .
  ```

  Si el output difiere, hay ficheros staged fuera del directorio de trabajo. Aborta el commit e informa al usuario.

- No hagas commits sin orden explícita del usuario.
- Terminar de implementar código no es autorización para hacer commit.
- No preguntes ni sugieras hacer commit al terminar una implementación.
- Si te piden hacer un commit, usa un mensaje corto, concreto y estructurado.
- No añadas trailers `Co-Authored-By` ni otros trailers de atribución automática salvo petición explícita del usuario.
- Nunca uses `$()`, `cat`, heredoc ni sustitución de comandos en `git commit`. Para mensajes multi-línea, usa múltiples flags `-m`.

## Comentarios de commit

Cuando se soliciten comentarios para commits, proporciona una línea concisa por cada cambio significativo. Usa formato directo y descriptivo, sin explicaciones largas.

```text
- Añadido control de duplicados con UNIQUE constraint en tabla alertas
- Implementado cron para generación automática de alertas
- Corregido timezone UTC en campos TIMESTAMP
```
