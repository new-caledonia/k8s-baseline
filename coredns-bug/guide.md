
https://crt.the-mori.com/programming/2020-03-18-coredns-connection-timeout-external-domain-name

```
# Store the ConfigMap into yaml file
kubectl get configmap coredns -n kube-system -o yaml > coredns.yaml

# Edit the config map to remove metadata to only include name and namespace
# change forward . /etc/resolv.conf to
# forward .  8.8.8.8 8.8.4.4
# be aware of 2 spaces after . 
vim coredns.yaml

# Deploy the new ConfigMap
kubectl apply -f coredns.yaml 

# Force update the CoreDNS deployment - review script below before executing!
sudo sh ./force-update-deployment.sh coredns -n kube-system
```
