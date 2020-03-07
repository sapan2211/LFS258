# SETUP DOCKER AND KUBERNETES

### Getting base ready 
```
sudo su
swapoff -a
vi /etc/ufw/sysctl.conf
	net/bridge/bridge-nf-call-ip6tables = 1
	net/bridge/bridge-nf-call-iptables = 1
	net/bridge/bridge-nf-call-arptables = 1
reboot
```

### installing docker and kubernetes
```
sudo su
apt-get update && apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF

apt-get update && apt-get install -y docker.io kubelet kubeadm kubectl
```

### Initialize kuberentes master
```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

### initiate the config for the user
```
whoami # if needed switch the user as needed 
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Flanel for networking
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```


### Add minions/slave nodes to the cluster
```
kubeadm join 172.31.10.0:6443 --token <token>  --discovery-token-ca-cert-hash <hash>
```

#### Other master operations
```
kubectl taint nodes --all node-role.kubernetes.io/master- #run this if you want to have single host master and minion, make master a minion as well
kubeadm token create --print-join-command # run this if you want to create new token for future to add new nodes/minions
```

### kubectl commands

