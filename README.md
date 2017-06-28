# Initial setup
Based on: https://www.packtpub.com/mapt/book/virtualization_and_cloud/9781787283367/1/ch01lvl1sec11/our-first-cluster

``` bash
sudo apt-get install phython curl
```

## Set up local Kubernetes cluster (Minikube)
https://kubernetes.io/docs/tasks/tools/install-minikube/
https://kubernetes.io/docs/getting-started-guides/minikube/#quickstart

### Set up KVM for Minikube
https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm-driver
``` bash
sudo apt-get install libvirt-bin qemu-kvm
# Debian/Ubuntu (NOTE: For Ubuntu 17.04 change the group to `libvirt`)
sudo usermod -a -G libvirtd $(whoami)
newgrp libvirtd
```

### Set up docker-machine
https://github.com/docker/machine/releases
``` bash
sudo apt-get install docker.io
curl -L https://github.com/docker/machine/releases/download/v0.12.0-rc2/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine
```

### Set up docker-machine-driver-kvm
https://github.com/dhiltgen/docker-machine-kvm/releases
``` bash
curl -L https://github.com/dhiltgen/docker-machine-kvm/releases/download/v0.10.0/docker-machine-driver-kvm-ubuntu16.04 > /tmp/docker-machine-driver-kvm && 
  chmod +x /tmp/docker-machine-driver-kvm &&
  sudo cp /tmp/docker-machine-driver-kvm /usr/local/bin/docker-machine-driver-kvm
```

### Set up kubectl
On Ubuntu: `sudo snap install kubectl --classic`  
Or using Google SDK: https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu
``` bash
export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)"
echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-get update && sudo apt-get install google-cloud-sdk
gcloud init
gcloud components install kubectl
```
Or using bash: `curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl`

### Install Minikube
https://kubernetes.io/docs/tasks/tools/install-minikube/
https://github.com/kubernetes/minikube/releases

``` bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.20.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

### Start minikube
``` bash
minikube start --vm-driver=kvm
```
kubectl cluster-info
kubectl config view
minikube dashboard
