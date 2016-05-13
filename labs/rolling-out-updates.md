# Rolling out Updates

Kubernetes makes it easy to rollout updates to your applications using the builtin rolling update mechanism. In this lab you will learn how to:

* Modify deployments to tigger rolling updates
* Pause and resume an active rolling update
* Rollback a deployment to a previous revision

## Tutorial: Rollout a new version of the Auth service

```
kubectl rollout history deployment auth
```

Modify the auth deployment image:

```
vim deployments/auth.yaml
```

```
image: "kelseyhightower/auth:2.0.0"
```

```
kubectl apply -f deployments/auth.yaml --record
```

```
kubectl describe deployments auth
```

```
kubectl get replicasets
```

```
kubectl rollout history deployment auth
```

## Tutorial: Pause and Resume an Active Rollout

```
kubectl rollout history deployment hello
```

Modify the hello deployment image:

```
vim deployments/hello.yaml
```

```
image: "kelseyhightower/hello:2.0.0"
```

```
kubectl apply -f deployments/hello.yaml --record
```

```
kubectl describe deployments hello
```

```
kubectl rollout pause deployment hello
```

```
kubectl rollout resume deployment hello
```

## Exercise: Rollback the Hello service

Use the `kubectl rollout undo` command to rollback to a previous deployment of the Hello service.

## Summary

In this lab you learned how to rollout updates to your applications by modifying deployment objects to trigger rolling updates. You also learned how to pause and resume an active rolling update and rollback it back using the `kubectl rollout` command.