# Guía de comandos Angular 17

Esta guía contiene comandos útiles para trabajar con **Angular 17** durante el desarrollo de una aplicación web, especialmente si estás siguiendo un curso Full Stack con Angular + Spring Boot.

---

## 1. Requisitos recomendados

Antes de crear el proyecto, verifica que tienes instalado Node.js y npm.

```bash
node -v
npm -v
```

Para Angular 17 se recomienda trabajar con una versión compatible de Node.js, por ejemplo Node 18 o Node 20.

---

## 2. Instalar Angular CLI 17

Instalar Angular CLI de forma global:

```bash
npm install -g @angular/cli@17
```

Verificar la versión instalada:

```bash
ng version
```

También puedes revisar la versión del CLI con:

```bash
ng v
```

---

## 3. Crear un nuevo proyecto Angular 17

Crear un proyecto Angular:

```bash
ng new nombre-del-proyecto
```

Ejemplo:

```bash
ng new angular-springboot-fullstack-app
```

Crear un proyecto sin instalar dependencias automáticamente:

```bash
ng new nombre-del-proyecto --skip-install
```

Crear un proyecto con routing:

```bash
ng new nombre-del-proyecto --routing
```

Crear un proyecto usando SCSS:

```bash
ng new nombre-del-proyecto --style=scss
```

Crear un proyecto con routing y SCSS:

```bash
ng new angular-springboot-fullstack-app --routing --style=scss
```

Entrar al proyecto:

```bash
cd angular-springboot-fullstack-app
```

Instalar dependencias si el proyecto fue creado con `--skip-install`:

```bash
npm install
```

---

## 4. Ejecutar el proyecto en local

Levantar el servidor de desarrollo:

```bash
ng serve
```

Ejecutar y abrir automáticamente en el navegador:

```bash
ng serve --open
```

Forma corta:

```bash
ng serve -o
```

Ejecutar en un puerto específico:

```bash
ng serve --port 4201
```

Ejecutar permitiendo acceso desde otra IP de la red:

```bash
ng serve --host 0.0.0.0
```

Ejecutar con host y puerto:

```bash
ng serve --host 0.0.0.0 --port 4201
```

---

## 5. Generar componentes

Crear un componente:

```bash
ng generate component nombre-componente
```

Forma corta:

```bash
ng g c nombre-componente
```

Ejemplo:

```bash
ng g c pages/home
```

Crear componente sin archivo de pruebas:

```bash
ng g c pages/home --skip-tests
```

Crear componente con SCSS:

```bash
ng g c pages/home --style=scss
```

Crear componente standalone:

```bash
ng g c pages/home --standalone
```

Crear componente dentro de una carpeta específica:

```bash
ng g c modules/products/pages/product-list
```

---

## 6. Generar servicios

Crear un servicio:

```bash
ng generate service nombre-servicio
```

Forma corta:

```bash
ng g s nombre-servicio
```

Ejemplo:

```bash
ng g s core/services/product
```

Crear servicio sin archivo de pruebas:

```bash
ng g s core/services/product --skip-tests
```

Ejemplo típico para consumir una API de Spring Boot:

```bash
ng g s core/services/customer
ng g s core/services/auth
ng g s core/services/product
```

---

## 7. Generar interfaces y modelos

Crear una interface:

```bash
ng generate interface nombre-interface
```

Forma corta:

```bash
ng g i nombre-interface
```

Ejemplo:

```bash
ng g i core/models/product
```

Crear una interface con tipo:

```bash
ng g i core/models/product model
```

Crear una clase:

```bash
ng generate class nombre-clase
```

Forma corta:

```bash
ng g class nombre-clase
```

Ejemplo:

```bash
ng g class core/models/customer
```

Crear un enum:

```bash
ng generate enum nombre-enum
```

Ejemplo:

```bash
ng g enum core/enums/order-status
```

---

## 8. Generar módulos

> Nota: Angular 17 trabaja muy bien con componentes standalone, pero en muchos cursos y proyectos empresariales todavía se usan módulos.

Crear un módulo:

```bash
ng generate module nombre-modulo
```

Forma corta:

```bash
ng g m nombre-modulo
```

Ejemplo:

```bash
ng g m modules/products
```

Crear módulo con routing:

```bash
ng g m modules/products --routing
```

Crear módulo y componente de página para lazy loading:

```bash
ng g m modules/products --route products --module app.routes
```

---

## 9. Generar rutas y guards

Crear un guard:

```bash
ng generate guard nombre-guard
```

Forma corta:

```bash
ng g guard nombre-guard
```

Ejemplo:

```bash
ng g guard core/guards/auth
```

Crear guards comunes:

```bash
ng g guard core/guards/auth
ng g guard core/guards/admin
ng g guard core/guards/no-auth
```

---

## 10. Generar interceptores HTTP

Crear un interceptor:

```bash
ng generate interceptor nombre-interceptor
```

Ejemplo:

```bash
ng g interceptor core/interceptors/auth
```

Crear interceptores comunes para una aplicación Full Stack:

```bash
ng g interceptor core/interceptors/auth
ng g interceptor core/interceptors/error
ng g interceptor core/interceptors/loading
```

Usos comunes:

- Agregar token JWT a las peticiones.
- Manejar errores HTTP globales.
- Mostrar u ocultar loader.
- Registrar logs de peticiones.

---

## 11. Generar pipes y directivas

Crear un pipe:

```bash
ng generate pipe nombre-pipe
```

Forma corta:

```bash
ng g pipe nombre-pipe
```

Ejemplo:

```bash
ng g pipe shared/pipes/currency-format
```

Crear una directiva:

```bash
ng generate directive nombre-directiva
```

Forma corta:

```bash
ng g directive nombre-directiva
```

Ejemplo:

```bash
ng g directive shared/directives/highlight
```

---

## 12. Instalar librerías frecuentes

Instalar Bootstrap:

```bash
npm install bootstrap
```

Instalar Angular Material:

```bash
ng add @angular/material
```

Instalar SweetAlert2:

```bash
npm install sweetalert2
```

Instalar PrimeNG:

```bash
npm install primeng primeicons
```

Instalar RxJS, normalmente ya viene con Angular:

```bash
npm install rxjs
```

Instalar JWT Decode:

```bash
npm install jwt-decode
```

Instalar Moment, aunque hoy suele recomendarse usar alternativas más modernas:

```bash
npm install moment
```

Instalar date-fns:

```bash
npm install date-fns
```

---

## 13. Consumir backend Spring Boot

Crear servicios para consumir endpoints REST:

```bash
ng g s core/services/api
ng g s core/services/auth
ng g s core/services/product
```

Ejemplo de estructura recomendada:

```text
src/app/
├── core/
│   ├── guards/
│   ├── interceptors/
│   ├── models/
│   └── services/
├── shared/
│   ├── components/
│   ├── pipes/
│   └── directives/
├── modules/
│   ├── auth/
│   ├── products/
│   └── customers/
└── app.routes.ts
```

Crear archivo de ambientes:

```bash
ng generate environments
```

Ejemplo de URL para backend local Spring Boot:

```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8080/api'
};
```

---

## 14. Configurar proxy para conectar Angular con Spring Boot

Crear archivo `proxy.conf.json` en la raíz del proyecto:

```json
{
  "/api": {
    "target": "http://localhost:8080",
    "secure": false,
    "changeOrigin": true
  }
}
```

Ejecutar Angular usando proxy:

```bash
ng serve --proxy-config proxy.conf.json
```

También puedes agregarlo en `package.json`:

```json
{
  "scripts": {
    "start": "ng serve --proxy-config proxy.conf.json"
  }
}
```

Luego ejecutar:

```bash
npm start
```

---

## 15. Build del proyecto

Compilar el proyecto:

```bash
ng build
```

Compilar para producción:

```bash
ng build --configuration production
```

Forma corta:

```bash
ng build -c production
```

Compilar y observar cambios:

```bash
ng build --watch
```

Ver archivos generados:

```bash
ls dist
```

---

## 16. Pruebas

Ejecutar pruebas unitarias:

```bash
ng test
```

Ejecutar pruebas sin modo watch:

```bash
ng test --watch=false
```

Ejecutar pruebas y generar reporte de cobertura:

```bash
ng test --code-coverage
```

Ejecutar pruebas end-to-end si el proyecto tiene configuración e2e:

```bash
ng e2e
```

---

## 17. Lint y formato

Angular CLI ya no instala TSLint por defecto en versiones modernas. Si el proyecto usa ESLint, puedes ejecutar:

```bash
ng lint
```

Instalar ESLint en Angular:

```bash
ng add @angular-eslint/schematics
```

Ejecutar lint con npm si está configurado en `package.json`:

```bash
npm run lint
```

Formatear con Prettier si está configurado:

```bash
npm run format
```

---

## 18. Actualizar Angular a versión 17

Ver versión actual:

```bash
ng version
```

Actualizar Angular Core y Angular CLI a la versión 17:

```bash
ng update @angular/core@17 @angular/cli@17
```

Actualizar Angular Material a la versión 17:

```bash
ng update @angular/material@17
```

Actualizar dependencias npm:

```bash
npm update
```

Limpiar dependencias y reinstalar:

```bash
rm -rf node_modules package-lock.json
npm install
```

En Windows PowerShell:

```powershell
Remove-Item -Recurse -Force node_modules
Remove-Item -Force package-lock.json
npm install
```

---

## 19. Comandos npm útiles

Instalar dependencias del proyecto:

```bash
npm install
```

Instalar una dependencia de producción:

```bash
npm install nombre-paquete
```

Instalar una dependencia de desarrollo:

```bash
npm install nombre-paquete --save-dev
```

Ejecutar script configurado en `package.json`:

```bash
npm run nombre-script
```

Ejemplo:

```bash
npm run start
npm run build
npm run test
```

Ver dependencias desactualizadas:

```bash
npm outdated
```

Actualizar dependencias:

```bash
npm update
```

Limpiar caché de npm:

```bash
npm cache clean --force
```

---

## 20. Comandos útiles para Git en un proyecto Angular

Inicializar repositorio:

```bash
git init
```

Ver estado:

```bash
git status
```

Agregar cambios:

```bash
git add .
```

Crear commit:

```bash
git commit -m "feat: initial angular 17 project"
```

Conectar repositorio remoto:

```bash
git remote add origin https://github.com/usuario/repositorio.git
```

Subir rama principal:

```bash
git branch -M main
git push -u origin main
```

---

## 21. Comandos recomendados para un proyecto Angular + Spring Boot

Crear proyecto Angular con routing y SCSS:

```bash
ng new angular-springboot-fullstack-app --routing --style=scss
```

Entrar al proyecto:

```bash
cd angular-springboot-fullstack-app
```

Crear estructura base:

```bash
ng g c shared/components/navbar --skip-tests
ng g c shared/components/footer --skip-tests
ng g c pages/home --skip-tests
ng g c pages/login --skip-tests
ng g c pages/not-found --skip-tests
```

Crear modelos:

```bash
ng g i core/models/user
ng g i core/models/product
ng g i core/models/customer
ng g i core/models/api-response
```

Crear servicios:

```bash
ng g s core/services/auth --skip-tests
ng g s core/services/product --skip-tests
ng g s core/services/customer --skip-tests
```

Crear guards:

```bash
ng g guard core/guards/auth
```

Crear interceptores:

```bash
ng g interceptor core/interceptors/auth
ng g interceptor core/interceptors/error
```

Ejecutar con proxy hacia Spring Boot:

```bash
ng serve --proxy-config proxy.conf.json
```

Compilar para producción:

```bash
ng build -c production
```

---

## 22. Tabla rápida de comandos

| Acción | Comando |
|---|---|
| Instalar Angular CLI 17 | `npm install -g @angular/cli@17` |
| Ver versión | `ng version` |
| Crear proyecto | `ng new nombre-proyecto` |
| Crear proyecto con routing y SCSS | `ng new nombre-proyecto --routing --style=scss` |
| Ejecutar proyecto | `ng serve` |
| Ejecutar y abrir navegador | `ng serve -o` |
| Crear componente | `ng g c ruta/nombre` |
| Crear servicio | `ng g s ruta/nombre` |
| Crear interface | `ng g i ruta/nombre` |
| Crear guard | `ng g guard ruta/nombre` |
| Crear interceptor | `ng g interceptor ruta/nombre` |
| Crear pipe | `ng g pipe ruta/nombre` |
| Crear directiva | `ng g directive ruta/nombre` |
| Crear módulo | `ng g m ruta/nombre` |
| Crear módulo con routing | `ng g m ruta/nombre --routing` |
| Crear environments | `ng generate environments` |
| Compilar | `ng build` |
| Compilar producción | `ng build -c production` |
| Ejecutar pruebas | `ng test` |
| Instalar Angular Material | `ng add @angular/material` |
| Actualizar a Angular 17 | `ng update @angular/core@17 @angular/cli@17` |

---

## 23. Buenas prácticas rápidas

- Usa nombres claros para componentes, servicios y modelos.
- Organiza el proyecto por carpetas: `core`, `shared`, `modules` y `pages`.
- Coloca la lógica de consumo de APIs en servicios.
- Usa interfaces para tipar las respuestas del backend.
- Usa interceptores para JWT y manejo global de errores.
- Usa guards para proteger rutas privadas.
- Configura proxy para evitar problemas de CORS durante desarrollo local.
- No subas `node_modules` al repositorio.
- Revisa que `.gitignore` incluya archivos generados y carpetas temporales.

---

## 24. Fuentes oficiales recomendadas

- Angular CLI: https://angular.dev/tools/cli
- Referencia de comandos Angular CLI: https://angular.dev/cli
- Instalación de Angular: https://angular.dev/installation
- Angular 17 CLI histórico: https://v17.angular.io/cli
- Compatibilidad de versiones: https://angular.dev/reference/versions

---

## 25. Ejemplo de `.gitignore` básico para Angular

```gitignore
# Dependencias
node_modules/

# Build
dist/
.angular/

# Logs
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Sistema operativo
.DS_Store
Thumbs.db

# IDEs
.vscode/
.idea/

# Environments sensibles
.env
```

---

## 26. Comandos finales más usados durante el curso

```bash
npm install -g @angular/cli@17
ng version
ng new angular-springboot-fullstack-app --routing --style=scss
cd angular-springboot-fullstack-app
ng serve -o
ng g c pages/home --skip-tests
ng g s core/services/product --skip-tests
ng g i core/models/product
ng g guard core/guards/auth
ng g interceptor core/interceptors/auth
ng serve --proxy-config proxy.conf.json
ng build -c production
```
