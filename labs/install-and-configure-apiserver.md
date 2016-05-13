# Install and configure the Kubernetes API Server

## node0

```
gcloud compute ssh node0
```

### Create the kube-apiserver systemd unit file:

```
[Unit]
Description=Kubernetes API Server
Documentation=https://github.com/GoogleCloudPlatform/kubernetes

[Service]
ExecStart=/usr/local/bin/hyperkube \
  apiserver \
  --insecure-bind-address=0.0.0.0 \
  --etcd-servers=http://127.0.0.1:2379 \
  --service-cluster-ip-range 10.32.0.0/24 \
  --allow-privileged=true
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Start the kube-apiserver service:

```
sudo mv kube-apiserver.service /etc/systemd/system/
```

```
sudo systemctl daemon-reload
sudo systemctl enable kube-apiserver
sudo systemctl start kube-apiserver
```

### Verify

```
sudo systemctl status kube-apiserver
kubectl version
kubectl get cs
```
