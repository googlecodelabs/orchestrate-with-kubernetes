# Download a Kubernetes Release

Offical Kubernetes releases are hosted on GitHub. We are going to download a copy of the official release from Google Cloud Storage hosted in the EU for performance.

```
wget https://storage.googleapis.com/craft-conf/kubernetes.tar.gz
tar -xvf kubernetes.tar.gz
tar -xvf kubernetes/server/kubernetes-server-linux-amd64.tar.gz
sudo cp kubernetes/server/bin/hyperkube /usr/local/bin/
sudo cp kubernetes/server/bin/kubectl /usr/local/bin/
```
