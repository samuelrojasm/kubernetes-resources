# Comandos de kubectl
Este archivo contiene una lista organizada de comandos útiles de **kubectl** para gestionar un clúster de Kubernetes en diferentes etapas del ciclo de vida del clúster. Los comandos están categorizados para facilitar su uso.

## Categorías
- [Comandos Básicos](#comandos-básicos)
- [Comandos de Gestión de Pods y Contenedores](#comandos-de-gestión-de-pods-y-contenedores)
- [Gestión de Recursos de Kubernetes](#gestión-de-recursos-de-kubernetes)
- [Comandos de Servicios y Networking](#comandos-de-servicios-y-networking)
- [Comandos de Administración y Mantenimiento](#comandos-de-administración-y-mantenimiento)
- [Comandos de Depuración](#comandos-de-depuración)
- [Operación Diaria](#operación-diaria)
- [Troubleshooting Diagnóstico y Resolución de Problemas)](#troubleshooting-diagnóstico-y-resolución-de-problemas)
- [Eliminar Recursos del Cluster](#eliminar-recursos-del-cluster)

## Comandos Básicos
### Obtener información del clúster
- `kubectl cluster-info` *(Ver detalles del clúster)*
- `kubectl get nodes` *(Obtener información sobre los nodos del clúster)*
- `kubectl describe nodes` *(Obtener información detallada de los nodos)*
### Ver recursos en el clúster
- `kubectl get pods --all-namespaces` *(Listar todos los pods en el clúster)*
- `kubectl get pods -n <namespace>` *(Listar todos los pods de un espacio de nombres específico)*
- `kubectl get pods -o wide` *(Listar más detalles de los pods)*
- `kubectl get services` *(Listar los servicios en el clúster)*
- `kubectl get deployments` *(Ver los deployments activos)*
- `kubectl get all -n <namespace>` *(Ver los recursos de un espacio de nombres específico)*
- `kubectl get all | grep <dato_nombre_recurso>` *(Ver un recurso específico)*
### Detalles de un recurso específico
- `kubectl describe pod <pod-name>` *(Describir un pod específico)*
- `kubectl describe service <service-name>` *(Describir un servicio específico)*

## Comandos de Gestión de Pods y Contenedores
### Crear y desplegar recursos
- `kubectl apply -f <archivo.yaml>` *(Crear un pod desde un archivo YAML)*
- `kubectl run <pod-name> --image=<image> --restart=Never` *(Crear un pod directamente desde la línea de comandos)*
- `kubectl delete pod <pod-name>` *(Eliminar un pod)*
- `kubectl scale deployment <deployment-name> --replicas=<num-replicas>` *(Escalar un Deployment)*
### Ver logs de un contenedor
- `kubectl logs <pod-name>` *(Ver los logs de un pod)*
- `kubectl logs <pod-name> -c <container-name>` *(Ver los logs de un contenedor específico dentro de un pod)*
- `kubectl logs -f <pod-name>` *(Ver los logs en tiempo real (seguimiento de logs))*
### Ejecutar comandos dentro de un pod
- `kubectl exec -it <pod-name> -- <comando>` *(Ejecutar un comando dentro de un contenedor en un pod)*
- `kubectl exec -it <pod-name> -- /bin/bash` *(Ejemplo para obtener una shell interactiva dentro de un pod)*
- `kubectl exec -it deployment/<deployment-name> -- <comando>` *(Ejecutar un comando en todos los pods de un deployment)*

## Gestión de Recursos de Kubernetes
### Crear y gestionar namespaces
- `kubectl create namespace <namespace-name>` *(Crear un nuevo namespace)*
- `kubectl get namespaces` *(Listar todos los namespaces)*
- `kubectl config set-context --current --namespace=<namespace-name>` *(Cambiar el contexto a un namespace específico)*
### ConfigMaps y Secrets
- `kubectl create configmap <configmap-name> --from-file=<path-to-file>` *(Crear un ConfigMap desde un archivo)*
- `kubectl create secret generic <secret-name> --from-file=<path-to-file>` *(Crear un Secret desde un archivo)*
- `kubectl get configmap <configmap-name> -o yaml` *(Ver un ConfigMap)*
- `kubectl get configmap <configmap-name> -o wide` *(Ver un ConfigMap con más detalles)*
- `kubectl get secret <secret-name> -o yaml` *(Ver un Secret (debidamente codificado))*

## Comandos de Servicios y Networking
### Exponer un recurso
- `kubectl expose pod <pod-name> --type=ClusterIP --name=<service-name>` *(Crear un servicio de tipo ClusterIP (por defecto))*
- `kubectl expose pod <pod-name> --type=LoadBalancer --name=<service-name>` *(Crear un servicio de tipo LoadBalancer (si es compatible con el entorno))*
- `kubectl expose pod <pod-name> --type=NodePort --name=<service-name>` *(Crear un servicio de tipo NodePort)*
### Ver servicios expuestos
- `kubectl get svc` *(Listar servicios en el clúster)*
- `kubectl describe svc <service-name>` *(Ver un servicio específico)*

## Comandos de Administración y Mantenimiento
### Actualizar recursos
- `kubectl set image deployment/<deployment-name> <container-name>=<new-image>` *(Actualizar un Deployment (por ejemplo, para cambiar la imagen del contenedor))*
- `kubectl apply -f <archivo.yaml>` *(Aplicar un manifiesto de configuración actualizado)*
- `kubectl rollout restart deployment <deployment-name>` *(Forzar la actualización de un pod dentro de un deployment)*
### Eliminar recursos
- `kubectl delete <resource-type> <resource-name>` *(Eliminar un pod, deployment o servicio)*
- `kubectl delete all --all -n <namespace-name>` *(Eliminar todos los recursos de un namespace)*
### Inspeccionar el estado de los recursos
- `kubectl get pods` *(Ver el estado de los pods)*
- `kubectl get deployments` *(Ver el estado de los deployments)*
- `kubectl get services` *(Ver el estado de los services)*
- `kubectl get events` *(Ver eventos en el clúster)*
### Ver la configuración del clúster
- `kubectl config view` *(Obtener la configuración actual de Kubernetes)*

## Comandos de Depuración
### Diagnóstico
- `kubectl describe pod <pod-name>` *(Ver el estado de un pod)*
- `kubectl get nodes` *(Obtener información del clúster y los nodos)*
- `kubectl logs <pod-name>` *(Ver los logs de un pod)*
- `kubectl logs -l app=<app-name>` *(Ver los logs de todos los pods (útil para debug de errores en múltiples pods))*

## Operación Diaria
Una vez que un clúster está en funcionamiento, esta categoría incluye comandos para gestionar el clúster, sus recursos, y realizar tareas diarias de mantenimiento y monitoreo.
### Gestionar Recursos de Kubernetes
- `kubectl get pods --all-namespaces` *(Ver los pods en todos los namespaces)*
- `kubectl apply -f deployment.yaml` *(Desplegar una nueva aplicación usando un archivo YAML)*
- `kubectl scale deployment <deployment-name> --replicas=3` *(Escalar un Deployment)*
- `kubectl logs <pod-name>` *(Ver los logs de un pod)*
- `kubectl expose pod <pod-name> --type=LoadBalancer --name=<service-name>` *(Crear un servicio para exponer un pod)*
### Actualización y Mantenimiento de Recursos
- `kubectl set image deployment/<deployment-name> <container-name>=<new-image>` *(Actualizar la imagen de un contenedor en un Deployment)*
- `kubectl rollout restart deployment <deployment-name>` *(Reiniciar un Deployment)*
- `kubectl rollout status deployment/<deployment-name>` *(Ver el estado del despliegue)*
- `kubectl get all` *(Obtener el estado de los recursos en el clúster)*
### Configuración de RBAC
- `kubectl get roles --all-namespaces` *(Ver roles en el clúster)*
- `kubectl get rolebindings --all-namespaces` *(Ver bindings en el clúster)*

## Troubleshooting Diagnóstico y Resolución de Problemas
Esta categoría incluye los comandos para diagnosticar y resolver problemas en un clúster de Kubernetes.
### Diagnóstico de Pods y Recursos
- `kubectl describe pod <pod-name>` *(Describir un pod y obtener información detallada)*
- `kubectl logs -f <pod-name>` *(Ver los logs de un contenedor en tiempo real)*
- `kubectl get events` *(Ver eventos del clúster)*
- `kubectl get pods --field-selector=status.phase!=Running` *(Comprobar la salud de los recursos)*
### Solución de Problemas de Red
- `kubectl get svc` *(Ver los servicios en el clúster)*
- `kubectl describe svc <service-name>` *(Ver detalles de un servicio)*
- `kubectl exec -it <pod-name> -- /bin/bash` *(Ejecutar un comando dentro de un pod para diagnóstico)*
### Solucionar Problemas de Conectividad
- `kubectl exec -it <pod-name> -- ping <target-ip>` *(Comprobar la conectividad de un pod (ejemplo con ping))*
- `kubectl top pod` *(Ver las métricas de los pods (si esta configurado Prometheus o Metrics Server))*

## Eliminar Recursos del Cluster
Cuando ya no se necesita un clúster de Kubernetes o se necesita destruir el entorno por completo, estos son los comandos que se pueden usar para eliminar recursos y destruir el clúster.
### Borrado de Recursos
- `kubectl delete pod <pod-name>` *(Eliminar un pod específico)*
- `kubectl delete deployment <deployment-name>` *(Eliminar un Deployment)*
- `kubectl delete svc <service-name>` *(Eliminar un servicio)*
- `kubectl delete all --all -n <namespace-name>` *(Eliminar todos los recursos en un namespace)*

## Recomendaciones
- Es posible usar el flag `-n <namespace>` para especificar un namespace en muchos comandos, si no se especifica, se usará el namespace `default`.
- Utilizar el flag `-o wide` para obtener más detalles sobre los recursos al usar comandos como `kubectl get`.
- La opción `-f <file>` permite trabajar con archivos YAML para definir o actualizar recursos.