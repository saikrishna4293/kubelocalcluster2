# How to Setup a Kubernetes Local cluster with vagrant

Here we have 
  * one master ubuntu <br />
  * two nodes ubuntu <br />

To launch 1 master and 2 nodes
```
Just run "vagrant up"
```
In here instead of going for flannel go for calico. So, that we can have a neat access to the pods <br />
After successful launch of the master and nodes <br />
## In master
```
vagrant ssh master
```
```
sudo kubeadm init --apiserver-advertise-address=192.168.56.20 --pod-network-cidr=192.168.0.0/16
```
#### Note: Save the output last 10 lines and execute 3 commands shown in stdout <br />
For calico reference (https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) <br />
After init we apply calico cni <br />
```
kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/rbac-kdd.yaml
kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/hosted/kubernetes-datastore/calico-networking/1.7/calico.yaml
```
You should now have some pods on your cluster and the master node should be ready <br />
```
kubectl get pods --all-namespaces
```
```
kubectl get nodes
```
master should be ready <br />

## In Node

```
vagrant ssh worker1
```
execute join command 
#### Do the same for worker 2 also
```
vagrant ssh worker2
```
execute join command 

### The cluster is now setup, Go to master and work your way, Happy Coding!


For original reference follow the below link 
### https://www.stratoscale.com/blog/kubernetes/installing-kubernetes-bare-metal/

