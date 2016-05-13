# Orchestrating the Cloud with Kuberenetes

In this Codelab you will learn how to:

* Provision a complete Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine)
* Deploy and manage Docker containers using kubectl

Kubernetes Version: 1.2.2

## Setup GCE and Enable Cloud Shell 

In this section you will create a Google Compute Engine (GCE) account. GCE will allow you to the create VMs, Networks, and Storage volumes required for this workshop. GCE also provides the [Cloud Shell](https://cloud.google.com/shell/docs) computing environment that will be used complete the labs.

#### Labs

  * [Create a GCE Account](labs/create-gce-account.md)
  * [Enable and explore Cloud Shell](labs/enable-and-explore-cloud-shell.md)

### Clone this Repository

Login into your Cloud Shell environment and clone this repository.

```
git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git
```

## Provision Kubernetes using GKE

Kubernetes is a distributed system composed of a collection of microservices. Like any system Kubernetes must be installed and configured. In this section you will install Kubernetes from the ground up with the minimal configuration required to get a cluster up and running.

Kubernetes can be configured with many options and add-ons, but can be time consuming to bootstrap from the ground up. In this section you will bootstrap Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine) (GKE).

  * [Provision a Kubernetes Cluster with GKE](labs/provision-kubernetes-cluster-with-gke.md)

## Managing Applications with Kubernetes

Kubernetes is all about applications and in this section you will utilize the Kubernetes API to deploy, manage, and upgrade applications. In this part of the workshop you will use an example application called "app" to complete the labs.

[App](https://github.com/kelseyhightower/app) is hosted on GitHub and provides an example 12 Facter application. During this workshop you will be working with the following Docker images:

* [kelseyhightower/monolith](https://hub.docker.com/r/kelseyhightower/monolith) - Monolith includes auth and hello services.
* [kelseyhightower/auth](https://hub.docker.com/r/kelseyhightower/auth) - Auth microservice. Generates JWT tokens for authenticated users.
* [kelseyhightower/hello](https://hub.docker.com/r/kelseyhightower/hello) - Hello microservice. Greets authenticated users.
* [ngnix](https://hub.docker.com/_/nginx) - Frontend to the auth and hello services.

#### Labs

For each of the following labs, you should be in the kubernetes dir:
```
cd orchestrate-with-kubernetes/kubernetes
```

  * [Creating and managing pods](labs/creating-and-managing-pods.md)
  * [Monitoring and health checks](labs/monitoring-and-health-checks.md)
  * [Managing application configurations and secrets](labs/managing-application-configurations-and-secrets.md)
  * [Creating and managing services](labs/creating-and-managing-services.md)
  * [Creating and managing deployments](labs/creating-and-managing-deployments.md)
  * [Rolling out updates](labs/rolling-out-updates.md)

## Links

  * [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
  * [gcloud Tool Guide](https://cloud.google.com/sdk/gcloud)
  * [Docker](https://docs.docker.com)
  * [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
  * [nginx](http://nginx.org)
