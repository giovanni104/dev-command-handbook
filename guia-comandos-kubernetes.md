# Comandos Básicos de Kubernetes

Guía rápida con comandos básicos de Kubernetes usando `kubectl`.

Este repositorio sirve como material de consulta para aprender, practicar y recordar comandos esenciales para trabajar con clústeres, namespaces, pods, deployments, services, configmaps, secrets y otros recursos de Kubernetes.

---

## ¿Qué es Kubernetes?

Kubernetes es una plataforma de orquestación de contenedores que permite desplegar, escalar, administrar y monitorear aplicaciones en contenedores.

Con Kubernetes puedes administrar aplicaciones distribuidas usando recursos como:

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets
- Namespaces
- Volumes
- Ingress
- Jobs
- CronJobs

---

## Verificar instalación de kubectl

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl version` | Muestra la versión del cliente y servidor Kubernetes | `kubectl version` |
| `kubectl version --client` | Muestra solo la versión del cliente kubectl | `kubectl version --client` |
| `kubectl cluster-info` | Muestra información del clúster | `kubectl cluster-info` |
| `kubectl config view` | Muestra la configuración actual de kubectl | `kubectl config view` |

---

## Contextos de Kubernetes

Un contexto define a qué clúster y usuario se conecta `kubectl`.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl config get-contexts` | Lista los contextos disponibles | `kubectl config get-contexts` |
| `kubectl config current-context` | Muestra el contexto actual | `kubectl config current-context` |
| `kubectl config use-context contexto` | Cambia al contexto indicado | `kubectl config use-context docker-desktop` |

---

## Namespaces

Los namespaces permiten separar recursos dentro de un clúster.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get namespaces` | Lista todos los namespaces | `kubectl get namespaces` |
| `kubectl get ns` | Forma corta para listar namespaces | `kubectl get ns` |
| `kubectl create namespace nombre` | Crea un namespace | `kubectl create namespace dev` |
| `kubectl delete namespace nombre` | Elimina un namespace | `kubectl delete namespace dev` |
| `kubectl config set-context --current --namespace=nombre` | Define un namespace por defecto en el contexto actual | `kubectl config set-context --current --namespace=dev` |

---

## Ver recursos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get all` | Lista los recursos principales del namespace actual | `kubectl get all` |
| `kubectl get all -n namespace` | Lista recursos principales de un namespace | `kubectl get all -n dev` |
| `kubectl get pods` | Lista pods del namespace actual | `kubectl get pods` |
| `kubectl get pods -n namespace` | Lista pods de un namespace específico | `kubectl get pods -n dev` |
| `kubectl get deployments` | Lista deployments | `kubectl get deployments` |
| `kubectl get services` | Lista servicios | `kubectl get services` |
| `kubectl get svc` | Forma corta para listar servicios | `kubectl get svc` |
| `kubectl get nodes` | Lista nodos del clúster | `kubectl get nodes` |
| `kubectl get events` | Lista eventos del namespace actual | `kubectl get events` |

---

## Ver recursos con más detalle

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get pods -o wide` | Lista pods con más información | `kubectl get pods -o wide` |
| `kubectl get svc -o wide` | Lista servicios con más información | `kubectl get svc -o wide` |
| `kubectl get deployment nombre -o yaml` | Muestra un deployment en formato YAML | `kubectl get deployment app -o yaml` |
| `kubectl get pod nombre -o yaml` | Muestra un pod en formato YAML | `kubectl get pod app-pod -o yaml` |
| `kubectl describe pod nombre` | Muestra detalles de un pod | `kubectl describe pod app-pod` |
| `kubectl describe deployment nombre` | Muestra detalles de un deployment | `kubectl describe deployment app` |
| `kubectl describe service nombre` | Muestra detalles de un servicio | `kubectl describe service app-service` |
| `kubectl describe node nombre` | Muestra detalles de un nodo | `kubectl describe node node-1` |

---

## Crear recursos desde línea de comandos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl create deployment nombre --image=imagen` | Crea un deployment | `kubectl create deployment nginx --image=nginx` |
| `kubectl expose deployment nombre --type=NodePort --port=puerto` | Expone un deployment como servicio | `kubectl expose deployment nginx --type=NodePort --port=80` |
| `kubectl run nombre --image=imagen` | Crea un pod simple | `kubectl run nginx-pod --image=nginx` |

---

## Aplicar archivos YAML

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl apply -f archivo.yaml` | Crea o actualiza recursos definidos en un YAML | `kubectl apply -f deployment.yaml` |
| `kubectl apply -f carpeta/` | Aplica todos los YAML de una carpeta | `kubectl apply -f k8s/` |
| `kubectl delete -f archivo.yaml` | Elimina recursos definidos en un YAML | `kubectl delete -f deployment.yaml` |

Ejemplo:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

## Eliminar recursos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl delete pod nombre` | Elimina un pod | `kubectl delete pod app-pod` |
| `kubectl delete deployment nombre` | Elimina un deployment | `kubectl delete deployment app` |
| `kubectl delete service nombre` | Elimina un servicio | `kubectl delete service app-service` |
| `kubectl delete namespace nombre` | Elimina un namespace | `kubectl delete namespace dev` |
| `kubectl delete all --all` | Elimina todos los recursos principales del namespace actual | `kubectl delete all --all` |

---

## Logs de pods

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl logs pod` | Muestra logs de un pod | `kubectl logs app-pod` |
| `kubectl logs -f pod` | Muestra logs en tiempo real | `kubectl logs -f app-pod` |
| `kubectl logs pod -c contenedor` | Muestra logs de un contenedor específico dentro del pod | `kubectl logs app-pod -c app-container` |
| `kubectl logs --tail=100 pod` | Muestra las últimas 100 líneas de logs | `kubectl logs --tail=100 app-pod` |
| `kubectl logs -n namespace pod` | Muestra logs de un pod en un namespace específico | `kubectl logs -n dev app-pod` |

---

## Entrar a un pod

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl exec -it pod -- bash` | Entra a un pod usando bash | `kubectl exec -it app-pod -- bash` |
| `kubectl exec -it pod -- sh` | Entra a un pod usando sh | `kubectl exec -it app-pod -- sh` |
| `kubectl exec pod -- comando` | Ejecuta un comando dentro del pod | `kubectl exec app-pod -- ls` |
| `kubectl exec -n namespace -it pod -- sh` | Entra a un pod en un namespace específico | `kubectl exec -n dev -it app-pod -- sh` |

---

## Deployments

Los deployments permiten administrar réplicas de una aplicación y realizar actualizaciones controladas.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get deployments` | Lista deployments | `kubectl get deployments` |
| `kubectl describe deployment nombre` | Muestra detalles del deployment | `kubectl describe deployment app` |
| `kubectl scale deployment nombre --replicas=n` | Cambia la cantidad de réplicas | `kubectl scale deployment app --replicas=3` |
| `kubectl set image deployment/nombre contenedor=imagen` | Actualiza la imagen del deployment | `kubectl set image deployment/app app=nginx:1.25` |
| `kubectl rollout status deployment/nombre` | Revisa el estado del despliegue | `kubectl rollout status deployment/app` |
| `kubectl rollout history deployment/nombre` | Muestra historial de despliegues | `kubectl rollout history deployment/app` |
| `kubectl rollout undo deployment/nombre` | Revierte al despliegue anterior | `kubectl rollout undo deployment/app` |
| `kubectl rollout restart deployment/nombre` | Reinicia los pods del deployment | `kubectl rollout restart deployment/app` |

---

## Services

Los services permiten exponer aplicaciones dentro o fuera del clúster.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get services` | Lista servicios | `kubectl get services` |
| `kubectl get svc` | Forma corta para listar servicios | `kubectl get svc` |
| `kubectl describe service nombre` | Muestra detalles del servicio | `kubectl describe service app-service` |
| `kubectl expose deployment nombre --port=puerto` | Expone un deployment como servicio | `kubectl expose deployment app --port=8080` |
| `kubectl expose deployment nombre --type=NodePort --port=puerto` | Expone usando NodePort | `kubectl expose deployment app --type=NodePort --port=8080` |

---

## Port Forward

`port-forward` permite acceder localmente a un pod o servicio del clúster.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl port-forward pod/pod puertoLocal:puertoPod` | Redirecciona un puerto local hacia un pod | `kubectl port-forward pod/app-pod 8080:8080` |
| `kubectl port-forward service/servicio puertoLocal:puertoServicio` | Redirecciona un puerto local hacia un servicio | `kubectl port-forward service/app-service 8080:8080` |
| `kubectl port-forward -n namespace service/servicio puertoLocal:puertoServicio` | Port forward a un servicio en un namespace | `kubectl port-forward -n dev service/app-service 8080:8080` |

---

## ConfigMaps

Los ConfigMaps permiten manejar configuración no sensible.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get configmaps` | Lista ConfigMaps | `kubectl get configmaps` |
| `kubectl get cm` | Forma corta para listar ConfigMaps | `kubectl get cm` |
| `kubectl create configmap nombre --from-literal=clave=valor` | Crea un ConfigMap desde una clave y valor | `kubectl create configmap app-config --from-literal=APP_ENV=dev` |
| `kubectl create configmap nombre --from-file=archivo` | Crea un ConfigMap desde un archivo | `kubectl create configmap app-config --from-file=application.properties` |
| `kubectl describe configmap nombre` | Muestra detalles de un ConfigMap | `kubectl describe configmap app-config` |
| `kubectl delete configmap nombre` | Elimina un ConfigMap | `kubectl delete configmap app-config` |

---

## Secrets

Los Secrets permiten manejar información sensible como contraseñas, tokens o llaves.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get secrets` | Lista Secrets | `kubectl get secrets` |
| `kubectl create secret generic nombre --from-literal=clave=valor` | Crea un Secret desde una clave y valor | `kubectl create secret generic app-secret --from-literal=DB_PASSWORD=123456` |
| `kubectl describe secret nombre` | Muestra detalles de un Secret | `kubectl describe secret app-secret` |
| `kubectl delete secret nombre` | Elimina un Secret | `kubectl delete secret app-secret` |

> **Importante:**  
> No subas Secrets reales a repositorios públicos.

---

## Jobs y CronJobs

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get jobs` | Lista Jobs | `kubectl get jobs` |
| `kubectl get cronjobs` | Lista CronJobs | `kubectl get cronjobs` |
| `kubectl describe job nombre` | Muestra detalles de un Job | `kubectl describe job batch-job` |
| `kubectl describe cronjob nombre` | Muestra detalles de un CronJob | `kubectl describe cronjob daily-job` |
| `kubectl delete job nombre` | Elimina un Job | `kubectl delete job batch-job` |
| `kubectl delete cronjob nombre` | Elimina un CronJob | `kubectl delete cronjob daily-job` |

---

## Ingress

Ingress permite exponer servicios HTTP/HTTPS fuera del clúster usando reglas de enrutamiento.

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get ingress` | Lista recursos Ingress | `kubectl get ingress` |
| `kubectl describe ingress nombre` | Muestra detalles de un Ingress | `kubectl describe ingress app-ingress` |
| `kubectl delete ingress nombre` | Elimina un Ingress | `kubectl delete ingress app-ingress` |

---

## Recursos y consumo

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl top nodes` | Muestra consumo de CPU y memoria de nodos | `kubectl top nodes` |
| `kubectl top pods` | Muestra consumo de CPU y memoria de pods | `kubectl top pods` |
| `kubectl top pods -n namespace` | Muestra consumo de pods en un namespace | `kubectl top pods -n dev` |

> Nota:  
> Para usar `kubectl top`, el clúster debe tener instalado Metrics Server.

---

## Copiar archivos entre local y pod

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl cp archivo pod:/ruta` | Copia un archivo local hacia un pod | `kubectl cp app.log app-pod:/tmp/app.log` |
| `kubectl cp pod:/ruta archivo` | Copia un archivo desde un pod hacia local | `kubectl cp app-pod:/tmp/app.log app.log` |
| `kubectl cp -n namespace archivo pod:/ruta` | Copia un archivo hacia un pod en un namespace | `kubectl cp -n dev app.log app-pod:/tmp/app.log` |

---

## Buscar y filtrar recursos

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get pods --show-labels` | Muestra pods con sus labels | `kubectl get pods --show-labels` |
| `kubectl get pods -l app=nombre` | Filtra pods por label | `kubectl get pods -l app=backend` |
| `kubectl get pods --field-selector=status.phase=Running` | Filtra pods por estado | `kubectl get pods --field-selector=status.phase=Running` |
| `kubectl get pods -A` | Lista pods de todos los namespaces | `kubectl get pods -A` |
| `kubectl get all -A` | Lista recursos principales de todos los namespaces | `kubectl get all -A` |

---

## Formatos de salida

| Comando | ¿Para qué sirve? | Ejemplo |
|---|---|---|
| `kubectl get pods -o wide` | Muestra información ampliada | `kubectl get pods -o wide` |
| `kubectl get pods -o yaml` | Muestra salida en YAML | `kubectl get pods -o yaml` |
| `kubectl get pods -o json` | Muestra salida en JSON | `kubectl get pods -o json` |
| `kubectl get pod pod -o jsonpath='{.status.phase}'` | Extrae un dato específico usando jsonpath | `kubectl get pod app-pod -o jsonpath='{.status.phase}'` |

---

## Ejemplo básico de Deployment

Archivo `deployment.yaml`:

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

Aplicar el deployment:

```bash
kubectl apply -f deployment.yaml
```

Ver pods:

```bash
kubectl get pods
```

---

## Ejemplo básico de Service

Archivo `service.yaml`:

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

Aplicar el servicio:

```bash
kubectl apply -f service.yaml
```

Ver servicios:

```bash
kubectl get svc
```

---

## Diagnóstico de errores comunes

### Ver estado general

```bash
kubectl get all
```

### Ver eventos

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

### Revisar detalle de un pod

```bash
kubectl describe pod nombre-pod
```

### Ver logs

```bash
kubectl logs -f nombre-pod
```

### Entrar al pod

```bash
kubectl exec -it nombre-pod -- sh
```

---

## Flujo básico diario con Kubernetes

```bash
kubectl config current-context
kubectl get ns
kubectl get pods -n dev
kubectl get deployments -n dev
kubectl logs -f nombre-pod -n dev
kubectl describe pod nombre-pod -n dev
```

---

## Flujo básico para desplegar una aplicación

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
kubectl get svc
kubectl logs -f nombre-pod
```

---

## Flujo básico para actualizar una imagen

```bash
kubectl set image deployment/app app=mi-imagen:1.0.1
kubectl rollout status deployment/app
kubectl rollout history deployment/app
```

Si necesitas revertir:

```bash
kubectl rollout undo deployment/app
```

---

## Comandos más usados en el día a día

| Comando | Uso principal |
|---|---|
| `kubectl get pods` | Ver pods |
| `kubectl get pods -n namespace` | Ver pods de un namespace |
| `kubectl get all` | Ver recursos principales |
| `kubectl describe pod nombre` | Ver detalle de un pod |
| `kubectl logs -f pod` | Ver logs en tiempo real |
| `kubectl exec -it pod -- sh` | Entrar a un pod |
| `kubectl apply -f archivo.yaml` | Crear o actualizar recursos |
| `kubectl delete -f archivo.yaml` | Eliminar recursos desde YAML |
| `kubectl get svc` | Ver servicios |
| `kubectl get deployments` | Ver deployments |
| `kubectl scale deployment app --replicas=3` | Escalar una aplicación |
| `kubectl rollout restart deployment/app` | Reiniciar pods de un deployment |
| `kubectl rollout undo deployment/app` | Revertir despliegue |
| `kubectl port-forward service/app 8080:8080` | Acceder localmente a un servicio |

---

## Recomendaciones

- Usa namespaces para separar ambientes como `dev`, `qa` y `prod`.
- Revisa siempre el contexto actual antes de ejecutar comandos importantes.
- Usa `kubectl get pods -n namespace` para validar el estado de tus pods.
- Usa `kubectl describe pod` cuando un pod esté en error.
- Usa `kubectl logs -f` para revisar errores de la aplicación.
- Usa archivos YAML para mantener la configuración versionada.
- No subas Secrets reales a repositorios públicos.
- Ten cuidado al ejecutar comandos de eliminación en namespaces productivos.

---

## Autor

**Giovanni Hernandez**

Repositorio creado como guía práctica para aprender y consultar comandos básicos de Kubernetes.

---

## Licencia

Este proyecto puede ser utilizado con fines educativos y de práctica.
