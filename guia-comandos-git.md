# Comandos Básicos de Git

Guía rápida con los comandos básicos de Git más usados en el día a día por desarrolladores.

Este repositorio sirve como material de consulta para aprender, practicar y recordar comandos esenciales de control de versiones.

---

## ¿Qué es Git?

Git es un sistema de control de versiones que permite guardar el historial de cambios de un proyecto, trabajar en equipo, crear ramas, versionar código y sincronizar cambios con plataformas como GitHub, GitLab o Bitbucket.

---

## Configuración inicial

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git config --global user.name "Tu Nombre"` | Configura el nombre del usuario | `git config --global user.name "Giovanni Hernandez"` |
| `git config --global user.email "correo@email.com"` | Configura el correo del usuario | `git config --global user.email "correo@email.com"` |
| `git config --list` | Muestra la configuración actual de Git | `git config --list` |

---

## Crear o clonar repositorios

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git init` | Inicializa Git en una carpeta local | `git init` |
| `git clone URL` | Descarga un repositorio remoto | `git clone https://github.com/usuario/proyecto.git` |

---

## Revisar estado y cambios

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git status` | Muestra el estado actual del repositorio | `git status` |
| `git diff` | Muestra los cambios realizados antes de agregarlos | `git diff` |
| `git log` | Muestra el historial de commits | `git log` |
| `git log --oneline` | Muestra el historial resumido | `git log --oneline` |

---

## Agregar cambios

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git add archivo` | Agrega un archivo específico al área de preparación | `git add README.md` |
| `git add .` | Agrega todos los archivos modificados | `git add .` |

---

## Crear commits

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git commit -m "mensaje"` | Guarda los cambios en el historial del proyecto | `git commit -m "Agrega documentación inicial"` |

### Ejemplos de buenos mensajes de commit

```bash
git commit -m "Agrega configuración inicial del proyecto"
git commit -m "Corrige error en validación de usuario"
git commit -m "Actualiza documentación de comandos Git"
git commit -m "Refactoriza servicio de autenticación"
```

---

## Trabajar con ramas

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git branch` | Lista las ramas locales | `git branch` |
| `git branch nombre-rama` | Crea una nueva rama | `git branch feature/login` |
| `git checkout nombre-rama` | Cambia a otra rama | `git checkout develop` |
| `git checkout -b nombre-rama` | Crea una rama y cambia a ella | `git checkout -b feature/login` |
| `git switch nombre-rama` | Cambia de rama usando el comando moderno | `git switch develop` |
| `git switch -c nombre-rama` | Crea una rama y cambia a ella usando el comando moderno | `git switch -c feature/login` |

---

## Fusionar ramas

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git merge nombre-rama` | Une una rama con la rama actual | `git merge feature/login` |

Ejemplo:

```bash
git checkout main
git merge feature/login
```

---

## Repositorios remotos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git remote -v` | Muestra los repositorios remotos configurados | `git remote -v` |
| `git remote add origin URL` | Conecta el repositorio local con un repositorio remoto | `git remote add origin https://github.com/usuario/proyecto.git` |

---

## Subir cambios al repositorio remoto

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git push origin rama` | Sube los cambios al repositorio remoto | `git push origin main` |
| `git push -u origin rama` | Sube una rama por primera vez y deja configurado el seguimiento | `git push -u origin feature/login` |

---

## Descargar cambios del repositorio remoto

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git pull` | Actualiza la rama actual desde el remoto configurado | `git pull` |
| `git pull origin rama` | Descarga y fusiona cambios de una rama remota específica | `git pull origin main` |
| `git fetch` | Descarga información del remoto sin fusionar automáticamente | `git fetch` |

---

## Actualizar la rama actual

Si quieres actualizar la rama donde estás trabajando actualmente, primero revisa el estado del repositorio:

```bash
git status
```

Luego actualiza la rama actual con:

```bash
git pull
```

Este comando descarga y fusiona los últimos cambios de la rama remota asociada a tu rama local.

### Actualizar indicando la rama

```bash
git pull origin nombre-de-tu-rama
```

Ejemplo:

```bash
git pull origin feature/login
```

### Si tienes cambios pendientes

Si tienes cambios sin guardar y no quieres hacer commit todavía, puedes usar `stash`:

```bash
git stash
git pull
git stash pop
```

Esto guarda temporalmente tus cambios, actualiza la rama y luego recupera tus cambios.

### Actualizar tu rama con cambios de `main`

Si estás trabajando en una rama como `feature/login` y quieres traer los últimos cambios de `main`:

```bash
git checkout main
git pull origin main
git checkout feature/login
git merge main
```

También puedes hacerlo desde tu rama actual:

```bash
git fetch origin
git merge origin/main
```

---

## Deshacer cambios

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git restore archivo` | Deshace los cambios locales de un archivo | `git restore README.md` |
| `git restore .` | Deshace todos los cambios locales no agregados | `git restore .` |
| `git reset archivo` | Quita un archivo del área de preparación, pero conserva los cambios | `git reset README.md` |
| `git reset --hard` | Elimina todos los cambios locales no confirmados | `git reset --hard` |

> **Importante:**  
> Usa `git reset --hard` con cuidado porque borra cambios locales que no han sido guardados en un commit.

---

## Eliminar archivos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `git rm archivo` | Elimina un archivo y registra el cambio en Git | `git rm archivo.txt` |

---

## Flujo básico de trabajo con Git

```bash
git status
git pull origin main
git checkout -b feature/nueva-funcionalidad
git add .
git commit -m "Agrega nueva funcionalidad"
git push -u origin feature/nueva-funcionalidad
```

---

## Flujo para actualizar tu rama actual

```bash
git status
git pull
```

Si tienes cambios pendientes:

```bash
git status
git stash
git pull
git stash pop
```

---

## Comandos más usados en el día a día

| Comando | Uso principal |
|---|---|
| `git status` | Revisar el estado del repositorio |
| `git add .` | Agregar todos los cambios |
| `git commit -m "mensaje"` | Guardar cambios en el historial |
| `git pull` | Descargar y fusionar cambios del remoto en la rama actual |
| `git fetch` | Descargar información del remoto sin fusionar automáticamente |
| `git push` | Subir cambios al remoto |
| `git branch` | Ver ramas |
| `git checkout -b nombre-rama` | Crear y cambiar a una nueva rama |
| `git switch -c nombre-rama` | Crear y cambiar a una nueva rama usando el comando moderno |
| `git merge nombre-rama` | Fusionar ramas |
| `git log --oneline` | Ver historial resumido |

---

## Recomendaciones

- Usa nombres de ramas claros.
- Escribe mensajes de commit descriptivos.
- Ejecuta `git status` frecuentemente.
- Antes de iniciar una tarea, descarga los últimos cambios con `git pull`.
- No trabajes directamente sobre `main` o `master` si estás en un equipo.
- Crea una rama por cada funcionalidad o corrección.
- Antes de hacer `git pull`, valida si tienes cambios pendientes.
- Usa `git stash` cuando necesites guardar cambios temporalmente sin hacer commit.

---

## Ejemplo de nombres de ramas

```bash
feature/login
feature/registro-usuario
bugfix/error-validacion
hotfix/correccion-produccion
docs/actualiza-readme
```

---

## Autor

**Giovanni Hernandez**

Repositorio creado como guía práctica para aprender y consultar comandos básicos de Git.

---

## Licencia

Este proyecto puede ser utilizado con fines educativos y de práctica.
