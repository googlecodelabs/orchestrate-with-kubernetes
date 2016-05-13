# Creating and Managing Deployments

Deployments abstract away the low level details of managing Pods. Pods are tied to the lifetime of the node they are created on. When the node goes away so does the Pod. ReplicaSets can be used to ensure one or more replicas of a Pods are always running, even when nodes fail.

Deployments sit on top of ReplicaSets and add the ability to define how updates to Pods should be rolled out.

In this lab we will combine everything we learned about Pods and Services to breakup the monolith application into smaller Services. You will create 3 deployments, one for each service:

* frontend 
* auth
* hello

You will also define internal services for the `auth` and `hello` deployments and an external service for the `frontend` deployment.

## Tutorial: Creating Deployments

### Create and Expose the Auth Deployment

```
kubectl create -f deployments/auth.yaml
```

```
kubectl describe deployments auth
```

```
kubectl create -f services/auth.yaml
```

### Create and Expose the Hello Deployment

```
kubectl create -f deployments/hello.yaml
```

```
kubectl describe deployments hello
```

```
kubectl create -f services/hello.yaml
```

### Create and Expose the Frontend Deployment


```
kubectl create configmap nginx-frontend-conf --from-file=nginx/frontend.conf
```

```
kubectl create -f deployments/frontend.yaml
```

```
kubectl create -f services/frontend.yaml
```

## Tutorial: Scaling Deployments

Behind the scenes Deployments manage ReplicaSets. Each deployment is mapped to one active ReplicaSet. Use the `kubectl get replicasets` command to view the current set of replicas.

```
kubectl get replicasets
```

ReplicaSets are scaled through the Deployment for each service and can be scaled independently. Use the `kubectl scale` command to scale the hello deployment:

```
kubectl scale deployments hello --replicas=3
```

```
kubectl describe deployments hello
```

```
kubectl get pods
```

```
kubectl get replicasets
```

## Exercise: Scaling Deployments

In this exercise you will scale the `frontend` deployment using an existing deployment configuration file.

### Hints

```
vim deployments/frontend.yaml
```

```
kubectl apply -f deployments/frontend.yaml
```

## Exercise: Interact with the Frontend Service

### Hints

```
kubectl get services frontend
```

```
curl -k https://<EXTERNAL-IP>
```

## Summary

Deployments are the preferred way to manage application deployments. You learned how to create, expose and scale deployments.