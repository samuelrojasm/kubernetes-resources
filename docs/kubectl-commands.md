# Comandos de kubectl
Este archivo contiene una lista organizada de comandos útiles de **kubectl** para gestionar un clúster de Kubernetes en diferentes etapas del ciclo de vida del clúster. Los comandos están categorizados para facilitar su uso.

## Categorías
- [Comandos Básicos](#comandos-básicos)
- [Comandos de Gestión de Pods y Contenedores](#comandos-de-gestión-de-pods-y-contenedores)



## Comandos Básicos
### Obtener información del clúster
- `kubectl cluster-info` *(Ver detalles del clúster)*
- `kubectl get nodes` *(Obtener información sobre los nodos del clúster)*
- `kubectl describe nodes` Obtener información detallada de los nodos 
### Ver recursos en el clúster
- `kubectl get pods --all-namespaces` Listar todos los pods en el clúster
- `kubectl get services` Listar los servicios en el clúster
- `kubectl get deployments` Ver los deployments activos
- `kubectl get all -n <namespace>` Ver los recursos de un espacio de nombres específico
### Detalles de un recurso específico
- `kubectl describe pod <pod-name>` Describir un pod específico
- `kubectl describe service <service-name>` Describir un servicio específico

## Comandos de Gestión de Pods y Contenedores
### Crear y desplegar recursos
- `kubectl apply -f <archivo.yaml>` Crear un pod desde un archivo YAML
- `kubectl run <pod-name> --image=<image> --restart=Never` Crear un pod directamente desde la línea de comandos
- `kubectl delete pod <pod-name>` Eliminar un pod
- `kubectl scale deployment <deployment-name> --replicas=<num-replicas>` Escalar un Deployment
### Ver logs de un contenedor
- `kubectl logs <pod-name>` Ver los logs de un pod
- `kubectl logs <pod-name> -c <container-name>` Ver los logs de un contenedor específico dentro de un pod
- `kubectl logs -f <pod-name>` Ver los logs en tiempo real (seguimiento de logs)
### Ejecutar comandos dentro de un pod
- `kubectl exec -it <pod-name> -- <comando>` Ejecutar un comando dentro de un contenedor en un pod
- `kubectl exec -it <pod-name> -- /bin/bash` Ejemplo para obtener una shell interactiva dentro de un pod
- `kubectl exec -it deployment/<deployment-name> -- <comando>` Ejecutar un comando en todos los pods de un deployment

## Gestión de Recursos de Kubernetes
### Crear y gestionar namespaces
- `kubectl create namespace <namespace-name>` Crear un nuevo namespace
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``
- ``

