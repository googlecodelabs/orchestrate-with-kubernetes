# Craft Kubernetes Workshop

In this workshop you will learn how to:

* Provision a basic Kubernetes cluster from the ground up using [Google Compute Engine](https://cloud.google.com/compute)
* Provision a complete Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine)
* Deploy and manage Docker containers using kubectl

Kubernetes Version: 1.2.2

## Google Compute Engine (GCE)

GCE will be used to setup a Kubernetes cluster from the ground up. This workshop will require the ability to create the following resources:

* Virtual Machines
* Routes
* Firewall Rules

### Setup GCE and Enable Cloud Shell 

In this section you will create a Google Compute Engine (GCE) account. GCE will allow you to the create VMs, Networks, and Storage volumes required for this workshop. GCE also provides the [Cloud Shell](https://cloud.google.com/shell/docs) computing environment that will be used complete the labs.

#### Labs


  * [Create a GCE Account](labs/create-gce-account.md)
  * [Enable and explore Cloud Shell](labs/enable-and-explore-cloud-shell.md)

### Clone this Repository

Login into your Cloud Shell environment and clone this repository.

```
git clone https://github.com/kelseyhightower/craft-kubernetes-workshop.git
```

## Provision a Kubernetes cluster from scratch

Kubernetes is a distributed system composed of a collection of microservices. Like any system Kubernetes must be installed and configured. In this section you will install Kubernetes from the ground up with the minimal configuration required to get a cluster up and running.

### Core Infrastructure

A Kubernetes cluster requires compute resources which can come from VMs or bare-metal machines, a container runtime environment such as Docker, and assumes the Kubernetes network model is in place.

#### Labs

  * [Provision Ubuntu on GCE](labs/provisioning-ubuntu-on-gce.md)
  * [Install and configure Docker](labs/install-and-configure-docker.md)
  * [Configure Networking](labs/configure-networking.md)

### Provision the Kubernetes Controller

Kubernetes can be broken up into two parts: the controller and worker nodes. The Kubernetes controller is where all cluster configuration is stored and is home to the Kubernetes API, Controller Manager, and Scheduler.

#### Labs

  * [Install and configure etcd](labs/install-and-configure-etcd.md)
  * [Download a Kubernetes release](labs/download-a-kubernetes-release.md)
  * [Install and configure the API Server](labs/install-and-configure-apiserver.md)
  * [Install and configure the Controller Manager](labs/install-and-configure-controller-manager.md)
  * [Install and configure the Scheduler](labs/install-and-configure-scheduler.md)

### Provision the Worker Nodes

Kubernetes worker nodes are responsible for running containers (inside of pods), service loadbalancing, and reporting status information and metrics for nodes and pods. In this section you will setup the Kubernetes worker nodes and install the following components:

* kubelet

#### Labs

  * [Install and configure the kubelet](labs/install-and-configure-kubelet.md)

## Provision Kubernetes using GKE

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
