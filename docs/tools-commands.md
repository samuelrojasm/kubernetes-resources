# Herramientas para Kubernetes

## Helm
Helm es un gestor de paquetes para Kubernetes que facilita la instalación, actualización y gestión de aplicaciones. Los **charts** son paquetes de recursos de Kubernetes empaquetados con todos los archivos necesarios para implementar una aplicación.

- Instalación de una aplicación con Helm:
```
helm install my-release <chart-name>
```

- Para actualizar una aplicación instalada con Helm:
```
helm upgrade my-release <chart-name>
```

## Kustomize
Kustomize es una herramienta para gestionar configuraciones de Kubernetes mediante la modificación y la personalización de archivos YAML. A diferencia de Helm, no utiliza plantillas, sino que permite modificar configuraciones existentes mediante la herencia. Ejemplo básico de uso:
```
kustomize build <path-to-directory> | kubectl apply -f -
```

## Carpenter
- Carpenter es un proyecto de código abierto que trabaja como un **provisionador de nodos dinámico para Kubernetes**. En términos sencillos, Carpenter ayuda a gestionar los nodos del clúster de manera más eficiente y dinámica, optimizando la capacidad de los nodos según la carga de trabajo del clúster y los requisitos de los pods que se están ejecutando.
- A diferencia de los provisionadores de nodos tradicionales de Kubernetes como Cluster Autoscaler, Carpenter se centra en la creación dinámica de nodos en lugar de ajustar únicamente el número de nodos existentes. Esto permite a Kubernetes provisionar nodos de forma más flexible y económica según las necesidades exactas de las aplicaciones y las cargas de trabajo.

### ¿Cómo funciona Carpenter?
Carpenter trabaja en estrecha colaboración con el **Kubernetes Scheduler** para determinar qué tipos de nodos (basados en capacidad de recursos, como CPU, memoria, etc.) deben ser creados para satisfacer los requisitos de los pods que están siendo programados. A continuación, Carpenter provisiona esos nodos de manera eficiente en función de las políticas de autoscaling definidas.

### ¿Cómo se configura Carpenter?
Carpenter es completamente configurable a través de recursos de Kubernetes, como **Provisioner**, que se utiliza para definir cómo debe comportarse Carpenter al crear nuevos nodos.
Ejemplo básico de un objeto Provisioner:
```
apiVersion: carpenter.sh/v1alpha1
kind: Provisioner
metadata:
  name: example-provisioner
spec:
  requirements:
    - key: "cpu"
      operator: "Gt"
      value: "4"  # Solo provisiona nodos con más de 4 CPUs
    - key: "memory"
      operator: "Gt"
      value: "16Gi"  # Solo provisiona nodos con más de 16Gi de memoria
  provider: aws  # El proveedor de la infraestructura, como AWS
  limits:
    resources:
      cpu: "1000"  # Límite de CPU total
      memory: "500Gi"  # Límite de memoria total
```
En este ejemplo:
- **requirements** especifica las características de los nodos que Carpenter debe provisionar.
- **provider** define la infraestructura en la que Carpenter provisionará nodos (en este caso, AWS).
- **limits** define los recursos máximos que Carpenter puede utilizar para la provisión de nodos

### Beneficios de usar Carpenter:
1. **Escalado eficiente:** Carpenter escala nodos solo cuando realmente es necesario, lo que reduce los costos al no mantener nodos innecesarios.
2. **Ahorro de costos:** La capacidad de crear nodos de manera dinámica y según las necesidades exactas de los pods puede reducir significativamente el costo de infraestructura.
3. **Flexibilidad:** Carpenter permite crear nodos con características específicas, lo que puede ser útil para cargas de trabajo con requisitos de recursos no convencionales (por ejemplo, GPUs, almacenamiento especializado).
4. **Optimización automática:** Los nodos se provisionan y eliminan automáticamente en función de la demanda del clúster, lo que facilita la gestión sin intervención manual.

### Casos de uso comunes de Carpenter:
- **Aplicaciones con cargas de trabajo variables:** Si tu carga de trabajo cambia con el tiempo (por ejemplo, picos de tráfico en ciertos momentos), Carpenter puede ajustar dinámicamente los nodos según las necesidades.
- **Provisión de nodos con características específicas:** Si tus aplicaciones requieren recursos específicos, como almacenamiento persistente o GPUs, Carpenter puede provisionar nodos con las configuraciones adecuadas.
- **Reducción de costos en infraestructuras en la nube:** Al eliminar nodos inactivos y no sobreprovisionar recursos, Carpenter ayuda a reducir los costos operativos en servicios de nube como AWS, GCP o Azure.