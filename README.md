## Expose deployment
```
kubectl expose deployment <deploymentname> --type=LoadBalancer --port 80 --target-port 80
```

## Autoscale deployment
```
kubectl autoscale deployment <deploymentname> --max 6 --min 4 --cpu-percent 50
```

## Troubleshoot pods
```
kubectl run curl --image=radial/busyboxplus:curl -n <namespace> -i --tty
```

## Delete evicted pods
```
kubectl get pods --all-namespaces| grep Evicted | $(awk '{print "kubectl -n " $1 " delete pod "$2}')
```

## Lable nodes
```
kubectl label nodes <nodename> kubernetes.io/role=worker
```

## Allow pods on masters
```
kubectl taint nodes --all node-role.kubernetes.io/master-
```

## Install helm
```
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

## Kubeadm join command
```
kubeadm token create --print-join-command
```

## Kubernetes dashboard token
```
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')
```

## Fix cluster-admin
```
kubectl [--namespace kube-system] create clusterrolebinding tiller-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
```
