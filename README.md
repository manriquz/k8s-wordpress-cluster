# WordPress on Kubernetes

Este repositorio contiene los manifiestos YAML necesarios para desplegar una aplicación WordPress con MySQL en un clúster de Kubernetes.

## Estructura del Repositorio

- `wordpress-deployment.yaml`: Despliegue de WordPress.  
- `mysql-deployment.yaml`: Despliegue de MySQL.  
- `wordpress-services.yaml`: Servicio para exponer WordPress vía NodePort.  
- `wordpress-pvc.yaml`: Claim de almacenamiento persistente para WordPress.  
- `wordpress-pv-fixed.yaml`: Volumen persistente para WordPress.  
- `wordpress-volume.yaml`: Volumen adicional para WordPress (si aplica).  

## Requisitos

- Kubernetes 1.29+  
- Container Runtime: containerd  
- CNI: Calico  
- 1 nodo master + 1 nodo worker  
- Ubuntu Server 22.04  

## Despliegue

```bash
kubectl apply -f mysql-deployment.yaml
kubectl apply -f wordpress-pv-fixed.yaml
kubectl apply -f wordpress-pvc.yaml
kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-services.yaml
```

## Acceso a WordPress

Una vez aplicados los manifiestos, WordPress estará accesible vía navegador desde la IP del nodo (master o worker) con el puerto del servicio NodePort.
Ejemplo de acceso:

http://`<IP-del-nodo>`:30080

Reemplaza `<IP-del-nodo>` por la dirección IP del nodo donde se desplegó el servicio (por ejemplo, `10.103.86.228`).


## Autor

César Manríquez  







