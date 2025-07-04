# WordPress en Kubernetes

Este repositorio contiene los manifiestos necesarios para desplegar una aplicación WordPress con MySQL en un clúster de Kubernetes, utilizando volúmenes persistentes (PVC), secretos, y servicios `NodePort`.

---

## Requisitos

- Kubernetes 1.29+  
- Container Runtime: containerd  
- CNI: Calico  
- 1 nodo master + 1 nodo worker  
- Ubuntu Server 22.04

---

## Estructura del Proyecto

```bash
.
├── mysql-deployment.yaml           # Despliegue de base de datos MySQL
├── wordpress-deployment.yaml       # Despliegue de WordPress
├── wordpress-pvc.yaml              # Volumen persistente de WordPress
├── wordpress-pv-fixed.yaml         # Volumen PV estático (opcional)
├── wordpress-services.yaml         # Servicio de WordPress vía NodePort
├── README.md                       # Documentación del proyecto
```
## Despliegue

```bash
kubectl apply -f mysql-deployment.yaml
kubectl apply -f wordpress-pv-fixed.yaml
kubectl apply -f wordpress-pvc.yaml
kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-services.yaml
```

## Acceso a WordPress

Una vez aplicados los manifiestos y con los pods en estado Running, WordPress estará accesible desde tu navegador con la IP del nodo worker y el puerto del servicio NodePort.

http://`<IP-del-nodo>`:30080

Reemplaza `<IP-del-nodo>` por la dirección IP del nodo donde se desplegó el servicio (por ejemplo, `10.103.86.228`).

## Credenciales

No se ha definido un usuario ni contraseña específicos para WordPress en el despliegue.

La instalación por defecto permite continuar con la configuración inicial vía navegador.

La contraseña del root de MySQL se gestiona mediante un Secret llamado mysql-pass, con el valor base64 de "password".

## Autor

César Manríquez  







