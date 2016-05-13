# Install and configure the Docker

In this lab you will install and configure Docker on node0 and node1. Docker is will run containers created by Kubernetes and provide the API required to inspect them.

### node0

```
gcloud compute ssh node0
```

### Create the Kubernetes Docker Bridge

By default Docker handles container networking for a Kubernetes cluster. Docker requires at least one bridge to be setup before running any containers. Each Docker host must have an unique bridge IP address to avoid allocating duplicate IP addresses to containers across hosts.

```
sudo ip link add name kubernetes type bridge
sudo ip addr add 10.200.0.1/24 dev kubernetes
sudo ip link set kubernetes up
```

### Install the Docker Engine

```
wget https://get.docker.com/builds/Linux/x86_64/docker-1.9.1
chmod +x docker-1.9.1
sudo mv docker-1.9.1 /usr/bin/docker
```

### Create the docker systemd unit file:

```
[Unit]
Description=Docker Application Container Engine
Documentation=http://docs.docker.io

[Service]
ExecStart=/usr/bin/docker daemon \
  --bridge=kubernetes \
  --iptables=false \
  --ip-masq=false \
  --host=unix:///var/run/docker.sock \
  --log-level=error \
  --storage-driver=overlay
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Copy the docker unit file into place.

```
sudo mv docker.service /etc/systemd/system/docker.service
```

Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

#### Verify

```
sudo systemctl status docker --no-pager
sudo docker version
```

### node1

```
gcloud compute ssh node1
```

### Create the Kubernetes Docker Bridge

```
sudo ip link add name kubernetes type bridge
sudo ip addr add 10.200.1.1/24 dev kubernetes
sudo ip link set kubernetes up
```

### Install the Docker Engine

```
wget https://get.docker.com/builds/Linux/x86_64/docker-1.9.1
chmod +x docker-1.9.1
sudo mv docker-1.9.1 /usr/bin/docker
```

### Create the docker systemd unit file

```
[Unit]
Description=Docker Application Container Engine
Documentation=http://docs.docker.io

[Service]
ExecStart=/usr/bin/docker daemon \
  --bridge=kubernetes \
  --iptables=false \
  --ip-masq=false \
  --host=unix:///var/run/docker.sock \
  --log-level=error \
  --storage-driver=overlay
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Copy the docker unit file into place.

```
sudo mv docker.service /etc/systemd/system/docker.service
```

Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

#### Verify

```
sudo systemctl status docker --no-pager
sudo docker version
```
