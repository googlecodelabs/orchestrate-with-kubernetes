# Install and configure etcd

Kubernetes cluster state is stored in etcd.

## node0

```
gcloud compute ssh node0
```

### Download etcd release

```
wget https://storage.googleapis.com/craft-conf/etcd-v2.3.2-linux-amd64.tar.gz
tar -xvf etcd-v2.3.2-linux-amd64.tar.gz
sudo cp etcd-v2.3.2-linux-amd64/etcdctl /usr/local/bin/
sudo cp etcd-v2.3.2-linux-amd64/etcd /usr/local/bin/
```

### Create the etcd systemd unit file:

```
[Unit]
Description=etcd
Documentation=https://github.com/coreos

[Service]
ExecStart=/usr/local/bin/etcd \
  --data-dir=/var/lib/etcd
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Start the etcd service:

```
sudo mv etcd.service /etc/systemd/system/
```

```
sudo systemctl daemon-reload
sudo systemctl enable etcd
sudo systemctl start etcd
```

### Verify

```
sudo systemctl status etcd
```

```
etcdctl cluster-health
```
