# Istio

## Install all necesary

```bash
#docker
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
sudo service docker start
sudo service docker enable
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo usermod -aG docker $(whoami)
sudo reboot
docker --version

#minikube
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virtinst virt-manager
sudo reboot

virt-host-validate
sudo apt install virtualbox virtualbox-dkms virtualbox-qt virtualbox-ext-pack
sudo apt update
vboxheadless --version

wget -O /tmp/minikube_latest.deb https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo apt install /tmp/minikube_latest.deb
minikube version

#kubectl
sudo snap install kubectl --classic
sudo reboot

#create cluster and nodes
minikube start --memory 4096
```

# Configutation

```bash
kubectl label namespace default istio-injection=enabled

minikube ip
#http://localhost:30080/

```

# Upgrade

```bash
kubectl -n istio-system set image deploy/jaeger jaeger=jaegertracing/all-in-one:1.24
kubectl -n istio-system set image deploy/kiali kiali=quay.io/kiali/kiali:v1.28
```
