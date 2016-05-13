# Monitoring and Health Checks

Kubernetes supports monitoring applications in the form of readiness and liveness probes. Health checks can be performed on each container in a Pod. Readiness probes indicate when a Pod is "ready" to serve traffic. Liveness probes indicate a container is "alive". If a liveness probe fails multiple times the container will be restarted. Liveness probes that continue to fail will cause a Pod to enter a crash loop. If a readiness check fails the container will be marked as not ready and will be removed from any load balancers.

In this lab you will deploy a new Pod named `healthy-monolith`, which is largely based on the `monolith` Pod with the addition of readiness and liveness probes.

In this lab you will learn how to:

* Create Pods with readiness and liveness probes
* Troubleshoot failing readiness and liveness probes

## Tutorial: Creating Pods with Liveness and Readiness Probes

Explore the `healthy-monolith` pod configuration file:

```
cat pods/healthy-monolith.yaml
```

Create the `healthy-monolith` pod using kubectl:

```
kubectl create -f pods/healthy-monolith.yaml
```

## Exercise: View Pod details

Pods will not be marked ready until the readiness probe returns an HTTP 200 response. Use the `kubectl describe` to view details for the `healthy-monolith` Pod.

### Hints

```
kubectl describe pods <pod-name>
```

### Quiz

* How is the readiness of the `healthy-monolith` Pod determined?
* How is the liveness of the `healthy-monolith` Pod determined?
* How often is the readiness probe checked?
* How often is the liveness probe checked?

> The `healthy-monolith` Pod logs each health check. Use the `kubectl logs` command to view them.

## Tutorial: Experiment with Readiness Probes

In this tutorial you will observe how Kubernetes responds to failed readiness probes. The `monolith` container supports the ability to force failures of it's readiness and liveness probes. This will enable us to simulate failures for the `healthy-monolith` Pod. 

Use the `kubectl port-forward` command to forward a local port to the health port of the `healthy-monolith` Pod.

```
kubectl port-forward healthy-monolith 10081:81
```

> You know have access to the /healthz and /readiness HTTP endpoints exposed by the monolith container.

### Experiment with Readiness Probes

Force the `monolith` container readiness probe to fail. Use the `curl` command to toggle the readiness probe status:

```
curl http://127.0.0.1:10081/readiness/status
```

Wait about 45 seconds and get the status of the `healthy-monolith` Pod using the `kubectl get pods` command:

```
kubectl get pods healthy-monolith
```

Use the `kubectl describe` command to get more details about the failing readiness probe:

```
kubectl describe pods healthy-monolith
```

> Notice the events for the `healthy-monolith` Pod report details about failing readiness probe.

Force the `monolith` container readiness probe to pass. Use the `curl` command to toggle the readiness probe status:

```
curl http://127.0.0.1:10081/readiness/status
```

Wait about 15 seconds and get the status of the `healthy-monolith` Pod using the `kubectl get pods` command:

```
kubectl get pods healthy-monolith
```

## Exercise: Experiment with Liveness Probes

Building on what you learned in the previous tutorial use the `kubectl port-forward` and `curl` commands to force the `monolith` container liveness probe to fail. Observe how Kubernetes responds to failing liveness probes.

### Hints

```
kubectl port-forward healthy-monolith 10081:81
```

```
curl http://127.0.0.1:10081/healthz/status
```

### Quiz

* What happened when the liveness probe failed?
* What events where created when the liveness probe failed?

## Summary

In this lab you learned that Kubernetes supports application monitoring using
liveness and readiness probes. You also learned how to add readiness and liveness probes to Pods and what happens when probes fail. 
