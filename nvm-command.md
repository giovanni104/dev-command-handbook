# NVM Commands Cheat Sheet

Guía rápida de comandos para administrar múltiples versiones de Node.js utilizando Node Version Manager (NVM).

## ¿Qué es NVM?

NVM (Node Version Manager) es una herramienta que permite instalar, administrar y cambiar entre diferentes versiones de Node.js en un mismo equipo.

---

# Instalación

## Windows

1. Descargar la última versión de NVM para Windows:
   https://github.com/coreybutler/nvm-windows/releases

2. Ejecutar `nvm-setup.exe`

3. Verificar instalación:

```bash
nvm version
```

---

# Comandos Básicos

## Listar versiones instaladas

```bash
nvm list
```

## Ver versiones disponibles para descargar

```bash
nvm list available
```

## Instalar una versión específica

```bash
nvm install 22.16.0
```

## Instalar la versión LTS

```bash
nvm install lts
```

## Cambiar a una versión instalada

```bash
nvm use 22.16.0
```

## Ver la versión activa

```bash
node -v
```

## Ver la versión de NPM

```bash
npm -v
```

## Desinstalar una versión

```bash
nvm uninstall 22.16.0
```

---

# Comandos Útiles

## Mostrar versión actual de Node

```bash
nvm current
```

## Mostrar todas las versiones instaladas

```bash
nvm ls
```

## Verificar la instalación

```bash
nvm version
```

---

# Comandos Avanzados

> Algunos de estos comandos funcionan únicamente en Linux/macOS y pueden no estar disponibles en NVM para Windows.

## Listar versiones remotas

```bash
nvm ls-remote
```

## Crear alias

```bash
nvm alias dev 22.16.0
```

## Mostrar alias configurados

```bash
nvm alias
```

## Eliminar alias

```bash
nvm unalias dev
```

## Establecer versión por defecto

```bash
nvm alias default 22.16.0
```

## Ejecutar script con una versión específica

```bash
nvm exec 22.16.0 app.js
```

## Ejecutar comando con una versión específica

```bash
nvm run 22.16.0 npm test
```

---

# Uso con Proyectos

## Crear archivo .nvmrc

Permite que un proyecto indique automáticamente qué versión de Node.js debe utilizar.

```bash
echo 22.16.0 > .nvmrc
```

## Utilizar versión definida en .nvmrc

```bash
nvm use
```

---

# Ejemplos Frecuentes

## Instalar última versión LTS

```bash
nvm install lts
```

## Activar última versión LTS

```bash
nvm use lts
```

## Verificar Node y NPM

```bash
node -v
npm -v
```

## Cambiar entre versiones

```bash
nvm use 18.20.8
nvm use 22.16.0
```

---

# Compatibilidad

| Sistema Operativo | Compatible |
|------------------|------------|
| Windows          | ✅ |
| Linux            | ✅ |
| macOS            | ✅ |

---

# Referencias

- NVM Windows: https://github.com/coreybutler/nvm-windows
- Node.js: https://nodejs.org
- NVM Linux/macOS: https://github.com/nvm-sh/nvm

---

## Autor

Basado en la recopilación de comandos publicada por **codewithleader** y enriquecida para facilitar su consulta y uso diario.
