Pods and Containers
===================

- Namespace: kubectl create namespace mem-example
- Secret for pulling private image: kubectl create secret docker-registry regsecret --docker-server=\<your-registry-server\> --docker-username=\<your-name\> --docker-password=\<your-pword\> --docker-email=\<your-email\>
	- \<your-registry-server\> is your Private Docker Registry FQDN.
	- \<your-name\> is your Docker username.
	- \<your-pword\> is your Docker password.
	- \<your-email\> is your Docker email
- Label nodes: kubectl label nodes \<your-node-name\> disktype=ssd
- Configmap-file: kubectl create configmap game-config --from-file=docs/user-guide/configmap/kubectl
- kubectl create configmap game-config-3 --from-file=\<my-key-name\>=\<path-to-file\>
	- kubectl create configmap game-config-3 --from-file=game-special-key=docs/user-guide/configmap/kubectl/game.properties
- Configmap-literal: kubectl create configmap special-config --from-literal=special.how=very --from-literal=special.type=charm

