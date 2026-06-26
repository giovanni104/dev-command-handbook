# Guía de instalación de Kubernetes en Windows con Docker Desktop

Esta guía explica cómo instalar y activar Kubernetes localmente en Windows usando Docker Desktop.

Está pensada para entornos de aprendizaje, desarrollo y pruebas locales.

---

## Tabla de contenido

- [Objetivo](#objetivo)
- [Requisitos previos](#requisitos-previos)
- [Paso 1: Verificar versión de Windows](#paso-1-verificar-versión-de-windows)
- [Paso 2: Instalar o actualizar WSL 2](#paso-2-instalar-o-actualizar-wsl-2)
- [Paso 3: Instalar Docker Desktop](#paso-3-instalar-docker-desktop)
- [Paso 4: Configurar Docker Desktop con WSL 2](#paso-4-configurar-docker-desktop-con-wsl-2)
- [Paso 5: Activar Kubernetes en Docker Desktop](#paso-5-activar-kubernetes-en-docker-desktop)
- [Paso 6: Verificar la instalación de Kubernetes](#paso-6-verificar-la-instalación-de-kubernetes)
- [Paso 7: Probar Kubernetes con Nginx](#paso-7-probar-kubernetes-con-nginx)
- [Paso 8: Instalar kubectl manualmente si es necesario](#paso-8-instalar-kubectl-manualmente-si-es-necesario)
- [Comandos útiles](#comandos-útiles)
- [Solución de errores comunes](#solución-de-errores-comunes)
- [Recomendaciones](#recomendaciones)
- [Referencias oficiales](#referencias-oficiales)

---

## Objetivo

Al finalizar esta guía tendrás un clúster local de Kubernetes funcionando en Windows usando Docker Desktop.

Podrás ejecutar comandos como:

```bash
kubectl get nodes
kubectl get pods
kubectl apply -f archivo.yaml
kubectl logs -f nombre-pod
```

---

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- Windows 10 o Windows 11.
- Virtualización habilitada en la BIOS.
- Conexión a internet.
- Permisos para instalar aplicaciones.
- Docker Desktop instalado o listo para instalar.
- WSL 2 habilitado.
- PowerShell o Windows Terminal.

---

## Paso 1: Verificar versión de Windows

Abre PowerShell y ejecuta:

```powershell
winver
```

También puedes revisar información del sistema con:

```powershell
systeminfo
```

Docker Desktop funciona mejor en Windows usando el backend de WSL 2.

---

## Paso 2: Instalar o actualizar WSL 2

Abre PowerShell como administrador y ejecuta:

```powershell
wsl --install
```

Si WSL ya está instalado, actualízalo:

```powershell
wsl --update
```

Verifica las distribuciones instaladas:

```powershell
wsl -l -v
```

Ejemplo de salida esperada:

```text
  NAME      STATE           VERSION
* Ubuntu    Running         2
```

Si tu distribución aparece con versión 1, cámbiala a WSL 2:

```powershell
wsl --set-version Ubuntu 2
```

Configura WSL 2 como versión predeterminada:

```powershell
wsl --set-default-version 2
```

---

## Paso 3: Instalar Docker Desktop

Descarga Docker Desktop desde la página oficial:

```text
https://www.docker.com/products/docker-desktop/
```

Durante la instalación:

1. Acepta los términos.
2. Mantén habilitada la opción de usar WSL 2.
3. Finaliza la instalación.
4. Reinicia el equipo si Docker Desktop lo solicita.

Luego abre Docker Desktop desde el menú de inicio de Windows.

---

## Paso 4: Configurar Docker Desktop con WSL 2

Abre Docker Desktop y ve a:

```text
Settings > General
```

Valida que esté activa la opción:

```text
Use the WSL 2 based engine
```

Luego ve a:

```text
Settings > Resources > WSL Integration
```

Activa la integración con tu distribución, por ejemplo:

```text
Ubuntu
```

Aplica los cambios con:

```text
Apply & Restart
```

Verifica Docker desde PowerShell:

```powershell
docker --version
docker version
docker info
```

También puedes probar Docker con:

```powershell
docker run hello-world
```

Si todo está bien, Docker descargará una imagen de prueba y ejecutará un contenedor.

---

## Paso 5: Activar Kubernetes en Docker Desktop

Docker Desktop permite crear un clúster local de Kubernetes.

### Opción nueva: desde la vista Kubernetes

En versiones recientes de Docker Desktop:

1. Abre Docker Desktop.
2. Ve a la vista **Kubernetes**.
3. Haz clic en **Create cluster**.
4. Selecciona el tipo de clúster:
   - `kubeadm`: clúster local de un solo nodo.
   - `kind`: permite clúster local de varios nodos.
5. Haz clic en **Create**.
6. Espera a que Docker Desktop descargue y configure los componentes.

### Opción clásica: desde Settings

En algunas versiones de Docker Desktop:

1. Abre Docker Desktop.
2. Ve a:

```text
Settings > Kubernetes
```

3. Marca la opción:

```text
Enable Kubernetes
```

4. Haz clic en:

```text
Apply & Restart
```

5. Espera hasta que aparezca el estado:

```text
Kubernetes running
```

> Nota:
> En Windows, la pestaña de Kubernetes no aparece si Docker Desktop está en modo de contenedores Windows. Debes usar Linux containers.

Para cambiar a Linux containers:

1. Busca el ícono de Docker en la barra de tareas.
2. Clic derecho.
3. Selecciona:

```text
Switch to Linux containers
```

---

## Paso 6: Verificar la instalación de Kubernetes

Abre PowerShell y ejecuta:

```powershell
kubectl version --client
```

Luego valida el contexto actual:

```powershell
kubectl config current-context
```

El contexto esperado normalmente es:

```text
docker-desktop
```

Si no estás usando el contexto de Docker Desktop, cámbialo con:

```powershell
kubectl config use-context docker-desktop
```

Verifica los nodos:

```powershell
kubectl get nodes
```

Salida esperada:

```text
NAME             STATUS   ROLES           AGE   VERSION
docker-desktop   Ready    control-plane   10m   v1.xx.x
```

Verifica los pods del sistema:

```powershell
kubectl get pods -A
```

---

## Paso 7: Probar Kubernetes con Nginx

Crea un deployment de prueba:

```powershell
kubectl create deployment nginx-demo --image=nginx
```

Verifica el deployment:

```powershell
kubectl get deployments
```

Verifica los pods:

```powershell
kubectl get pods
```

Expón la aplicación usando un servicio:

```powershell
kubectl expose deployment nginx-demo --type=NodePort --port=80
```

Verifica el servicio:

```powershell
kubectl get svc
```

También puedes acceder usando port-forward:

```powershell
kubectl port-forward deployment/nginx-demo 8080:80
```

Luego abre en tu navegador:

```text
http://localhost:8080
```

Deberías ver la página de bienvenida de Nginx.

Para eliminar la prueba:

```powershell
kubectl delete service nginx-demo
kubectl delete deployment nginx-demo
```

---

## Paso 8: Instalar kubectl manualmente si es necesario

Docker Desktop normalmente instala `kubectl` automáticamente.

Puedes verificarlo con:

```powershell
kubectl version --client
```

Si el comando no existe, puedes instalarlo con `winget`:

```powershell
winget install -e --id Kubernetes.kubectl
```

También puedes instalarlo con Chocolatey:

```powershell
choco install kubernetes-cli
```

O con Scoop:

```powershell
scoop install kubectl
```

Después verifica:

```powershell
kubectl version --client
```

---

## Comandos útiles

### Ver contexto actual

```powershell
kubectl config current-context
```

### Cambiar al contexto de Docker Desktop

```powershell
kubectl config use-context docker-desktop
```

### Ver nodos

```powershell
kubectl get nodes
```

### Ver pods

```powershell
kubectl get pods
```

### Ver pods de todos los namespaces

```powershell
kubectl get pods -A
```

### Ver servicios

```powershell
kubectl get svc
```

### Ver deployments

```powershell
kubectl get deployments
```

### Ver recursos principales

```powershell
kubectl get all
```

### Ver detalles de un pod

```powershell
kubectl describe pod nombre-pod
```

### Ver logs de un pod

```powershell
kubectl logs nombre-pod
```

### Ver logs en tiempo real

```powershell
kubectl logs -f nombre-pod
```

### Entrar a un pod

```powershell
kubectl exec -it nombre-pod -- sh
```

### Aplicar un archivo YAML

```powershell
kubectl apply -f archivo.yaml
```

### Eliminar recursos desde YAML

```powershell
kubectl delete -f archivo.yaml
```

---

## Ejemplo de archivo deployment.yaml

Crea un archivo llamado `deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-demo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app-demo
  template:
    metadata:
      labels:
        app: app-demo
    spec:
      containers:
        - name: app-demo
          image: nginx:latest
          ports:
            - containerPort: 80
```

Aplica el archivo:

```powershell
kubectl apply -f deployment.yaml
```

Verifica:

```powershell
kubectl get pods
kubectl get deployments
```

---

## Ejemplo de archivo service.yaml

Crea un archivo llamado `service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: app-demo-service
spec:
  type: NodePort
  selector:
    app: app-demo
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

Aplica el servicio:

```powershell
kubectl apply -f service.yaml
```

Verifica:

```powershell
kubectl get svc
```

Accede desde el navegador:

```text
http://localhost:30080
```

Para eliminar los recursos:

```powershell
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
```

---

## Solución de errores comunes

### Error: kubectl no se reconoce como comando

Verifica si Docker Desktop instaló `kubectl`:

```powershell
where kubectl
```

Si no aparece, instala `kubectl`:

```powershell
winget install -e --id Kubernetes.kubectl
```

Cierra y abre nuevamente la terminal.

---

### Error: Kubernetes no inicia en Docker Desktop

Intenta lo siguiente:

1. Reinicia Docker Desktop.
2. Verifica que estés usando Linux containers.
3. Verifica que WSL 2 esté activo.
4. Aumenta recursos de Docker Desktop.

Ruta recomendada:

```text
Docker Desktop > Settings > Resources
```

Puedes asignar más memoria y CPU si tu equipo lo permite.

---

### Error: kubectl apunta a otro clúster

Revisa el contexto actual:

```powershell
kubectl config current-context
```

Lista todos los contextos:

```powershell
kubectl config get-contexts
```

Cambia al contexto de Docker Desktop:

```powershell
kubectl config use-context docker-desktop
```

---

### Error: No resources found

Puede ser normal si aún no has desplegado nada en el namespace actual.

Valida todos los namespaces:

```powershell
kubectl get pods -A
```

---

### Error: ImagePullBackOff

Este error indica que Kubernetes no pudo descargar la imagen.

Revisa el detalle del pod:

```powershell
kubectl describe pod nombre-pod
```

Causas comunes:

- Nombre de imagen incorrecto.
- Tag inexistente.
- Problemas de conexión a internet.
- Imagen privada sin credenciales.

---

### Error: CrashLoopBackOff

Este error indica que el contenedor inicia y se cae repetidamente.

Revisa logs:

```powershell
kubectl logs nombre-pod
```

Revisa eventos:

```powershell
kubectl describe pod nombre-pod
```

---

### Resetear Kubernetes en Docker Desktop

Si el clúster local queda dañado o no inicia, puedes resetearlo.

Ruta:

```text
Docker Desktop > Settings > Kubernetes > Reset Kubernetes Cluster
```

O desde la sección de troubleshooting de Docker Desktop:

```text
Docker Desktop > Troubleshoot > Reset Kubernetes cluster
```

> Importante:
> Esta acción elimina recursos del clúster local de Kubernetes.

---

## Recomendaciones

- Usa Docker Desktop Kubernetes solo para desarrollo y pruebas locales.
- No lo uses como reemplazo de un clúster productivo.
- Revisa siempre el contexto antes de ejecutar comandos importantes.
- Usa archivos YAML para versionar tus deployments y services.
- No subas secrets reales a repositorios públicos.
- Usa namespaces para separar ambientes locales como `dev`, `qa` o `test`.
- Si trabajas con Spring Boot, valida primero que la imagen Docker funcione antes de desplegarla en Kubernetes.
- Si un pod falla, empieza revisando:

```powershell
kubectl describe pod nombre-pod
kubectl logs nombre-pod
```

---

## Flujo rápido de instalación

```powershell
wsl --install
wsl --update
wsl -l -v
docker --version
docker run hello-world
kubectl config use-context docker-desktop
kubectl get nodes
kubectl get pods -A
```

---

## Flujo rápido de prueba

```powershell
kubectl create deployment nginx-demo --image=nginx
kubectl expose deployment nginx-demo --type=NodePort --port=80
kubectl get pods
kubectl get svc
kubectl port-forward deployment/nginx-demo 8080:80
```

Abrir en el navegador:

```text
http://localhost:8080
```

Eliminar prueba:

```powershell
kubectl delete service nginx-demo
kubectl delete deployment nginx-demo
```

---

## Referencias oficiales

- Docker Desktop para Windows:  
  https://docs.docker.com/desktop/setup/install/windows-install/

- Docker Desktop con WSL 2:  
  https://docs.docker.com/desktop/features/wsl/

- Kubernetes en Docker Desktop:  
  https://docs.docker.com/desktop/use-desktop/kubernetes/

- Configuración de Kubernetes en Docker Desktop:  
  https://docs.docker.com/desktop/settings-and-maintenance/settings/#kubernetes

- Instalar kubectl en Windows:  
  https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

---

## Autor

**Giovanni Hernandez**

Guía creada como material de consulta para instalar y usar Kubernetes localmente en Windows con Docker Desktop.

---

## Licencia

Este material puede ser utilizado con fines educativos y de práctica.
