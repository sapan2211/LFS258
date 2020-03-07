# SETUP DOCKER AND KUBERNETES

```
sudo su
swapoff -a
vi /etc/ufw/sysctl.conf
	net/bridge/bridge-nf-call-ip6tables = 1
	net/bridge/bridge-nf-call-iptables = 1
	net/bridge/bridge-nf-call-arptables = 1
reboot
```

sudo su
apt-get update && apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF

apt-get update && apt-get install -y docker kubelet kubeadm kubectl docker.io

kubeadm init --pod-network-cidr=10.244.0.0/16
exit
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml


kubectl taint nodes --all node-role.kubernetes.io/master-


kubectl run hello --image=k8s.gcr.io/echoserver:1.4 --port=8080

kubectl get po --all-namespaces

kubeadm join 172.31.10.0:6443 --token sccnnm.nann3kgybp8cy2o6     --discovery-token-ca-cert-hash sha256:4518e7e19756360042f0fb9e0dfd0834050583e60aa9cacdbd39229c390085e9



get sha256: openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
kubeadm join 172.31.10.0:6443 --token sccnnm.nann3kgybp8cy2o6     --discovery-token-ca-cert-hash sha256:53733d87040188e2d5ec99166b9278effe0d4fc982449c7e8c36957df24eadbf



kubeadm token create --print-join-command



From remote kubectl
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl config set-cluster kubernetes --server=https://18.188.129.221:6443


kubectl config set-cluster kubernetes --server=https://18.188.129.221:6443 --certificate-authority=~/.kube/ca.pem 

kubectl config set-credentials kubernetes-admin \
    --certificate-authority=~/.kube/ca.pem \
    --client-key=~/.kube/admin-key.pem \
    --client-certificate=~/.kube/admin.pem 
	
kubectl config set-context kubernetes-admin@kubernetes --cluster=kubernetes --user=kubernetes-admin

kubectl config use-context kubernetes-admin@kubernetes
