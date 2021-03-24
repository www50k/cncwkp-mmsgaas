### Creating a MMSGAAS (Managed Messaging as a Service)

1. Create a Docker Image with ActiveMQ Artemis.

```
docker build -t cloops/mmsgaas-app:latest .
docker push cloops/mmsgaas-app:latest
docker run -p 8088:8080 -d cloops/mmsgaas:lates
```

2. Create Kubernetes Deployment and Service for ActiveMQ Artemis.

```
kubectl apply -f mmsgaas-app/deployment.yaml
kubectl port-forward service/mmsgaas-app 8080:8080 --namespace=mmsgaas
kubectl get pods,svc --namespace=mmsgaas
kubectl port-forward service/mmsgaas-app 8080:8080 --namespace=mmsgaas
```

3. Create Ingress to access ActiveMQ Artemis Endpoints.

4. Deploy Nngix Ingress Controller.

```
minikube addons enable ingress
```

5. Create Kubernetes Ingress for ActiveMQ Artemis Dashboard (88161) and openwire (61616)


