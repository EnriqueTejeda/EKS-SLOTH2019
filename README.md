# SLOTH 2019 DEMO 


## Requisitos
* aws-cli  y configurar accesos (aws configure) [Instalar](https://aws.amazon.com/es/cli/)
* aws-iam-authenticator [Instalar](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)
* kubectl [Instalar](https://kubernetes.io/es/docs/tasks/tools/install-kubectl/)
* maven  
* jre runtime (Java) 

## Docker

### Crear Fat-Jar de nuestra aplicacion Vert.X
```
mvn package
```

### Construir Imagen Docker
```
docker build -t sample/vertx-java-fat .
```

## Terraform

### Getting Started
```
terraform init
```
### Deploy 
```
terraform plan
terraform apply
```
### Setting Up kubectl
```
mkdir ~/.kube/
terraform output kubeconfig>~/.kube/config
```
### Setting Up ConfigMap
```
terraform output config_map_aws_auth > configmap.yml
kubectl apply -f configmap.yml
```

## Kubernetes

### Creamos namespace 
```
kubectl apply -f sloth-namespace.yml
```
### Instalacion ALB Ingress Controller y RBAC Roles
```
kubectl apply -f ALB/alb-ingress-controller.yaml
kubectl apply -f ALB/rbac-role.yaml
```
### Deployment FrontEnd
```
kubectl apply -f FRONTEND/front.yml
```
### Deployment FrontEnd Service
```
kubectl apply -f FRONTEND/front-service.yml
```
### Deployment Ingress (Balanceador de Aplicacion)
```
kubectl apply -f INGRESS/ingress.yml
```
### Borrar pods, services, deployments

```
# delete all pods
kubectl delete --all pods --namespace=default

# delete all deployments
 kubectl delete --all deployments --namespace=default

 # delete all services
kubectl delete --all services --namespace=default
```



### Resources
* [ Docker Hub Image ](https://hub.docker.com/r/etejeda/sloth-vertx-demo)
* [ Amazon EKS Workshop ](https://eksworkshop.com/)
* [ Amazon EKS ALB Controller ](https://docs.aws.amazon.com/es_es/eks/latest/userguide/alb-ingress.html)

