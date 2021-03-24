### Creating a MMSGAAS (Managed Messaging as a Service)

1. Start & Install `ingress` addon to `minikube` to enable ingress-nginx controller.
```
$ cd <location on workshop code>
$ minikube start
$ minikube addons enable ingress
$ kubectl get pods -o wide --namespace=kube-system
$ minikube dashboard
```

2. Pull Docker Images
```
$ docker pull cloops/mmsgaas-bus:latest
$ docker pull cloops/mmsgaas-app:v0.10
```

3. Clone CNC Workshop - MMSGAAS Sample
```
$ git clone https://github.com/www50k/cncwkp-mmsgaas.git
cd cncwkp-mmsgaas
```

4. Create `mmsgaas` Namespace, Persistent Volume and Persistent Volume Claims. 
```
$ cd cncwkp-mmsgaas
$ kubectl apply -f mmsgaas-env/namespace.yaml
$ kubectl apply -f mmsgaas-env/mmsgaas-env/pv.yaml
$ kubectl apply -f mmsgaas-env/mmsgaas-env/pvc.yaml
```

5. Deploy Messaging Bus `mmsgaas-bus`
```
$ kubectl apply -f mmsgaas-bus/deployment.yaml
$ kubectl apply -f mmsgaas-bus/ingress-dash.yaml
$ kubectl get svc mmsgaas-bus -o wide --namespace=mmsgaas # Copy & Store `CLUSTER-IP` #
```

6. Deploy App in a APIServer `mmsgaas-app`
```
$ Update file `mmsgaas-app/configMap.yaml` with copied `CLUSTER-IP` in step 5
$ kubectl apply -f mmsgaas-app/configMap.yaml
$ kubectl apply -f mmsgaas-app/secret.yaml
$ kubectl apply -f mmsgaas-app/deployment.yaml
$ kubectl apply -f mmsgaas-app/ingress-api.yaml
```

7. Add ingress hostnames to end of the hosts file (/etc/hosts)
```
$ minikube ip # Lookup minikube IP #
$ sudo vi /etc/hosts
# Added for CNC Workshop
<minikube IP> dashboard.cloud.mmsgaas
<minikube IP> restapi.cloud.mmsgaas
```

8. Access Active MQ dashboard in browser
```
http://dashboard.cloud.mmsgaas/
```

9. Publish a message to `queue` on REST endpoint.
```
$ curl -X POST -d "I am now a PRO with CNC Concepts" http://restapi.cloud.mmsgaas/send
```

10. Check `Queue` attributes to check published message stats.
