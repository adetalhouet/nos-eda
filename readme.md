# Multi-vendor close-loop automation with Event-Driven Ansible

This demonstration uses [kne](https://github.com/openconfig/kne/tree/main) to create the networking topology. It uses [gnmic](https://github.com/openconfig/gnmic) for telemetry and a kafka bus where Event Driven Ansible listens to event.

### requirements
- go 1.21

### install kne
git clone https://github.com/openconfig/kne.git
git checkout v0.1.15
make install
mv kne ~/.local/bin/
kne version

### deploy meshnet cni
https://github.com/raballew/kne-on-ocp#deploy-meshnet-cni

### install kne vendor controllers

#### Arista

```
oc apply -f https://raw.githubusercontent.com/aristanetworks/arista-ceoslab-operator/v2.0.2/config/kustomized/manifest.yaml
```
Provide privileges to the Arista controller; see https://github.com/aristanetworks/arista-ceoslab-operator/issues/5
```
oc adm policy add-scc-to-user privileged system:serviceaccount:srlinux-controller:srlinux-controller-controller-manager
```

#### Nokia

```
oc apply -k https://github.com/srl-labs/srl-controller/config/default?ref=v0.6.0
```
Provide privileges to the Nokia controller
```
oc adm policy add-scc-to-user privileged system:serviceaccount:arista-ceoslab-operator-system:arista-ceoslab-operator-controller-manager
```

### deploy topology

Will deploy in `kne-multivendor` namespace
```
kne create multivendor.pb.txt
```




###### Misc links
https://github.com/raballew/kne-on-ocp/tree/main
https://cloud.redhat.com/blog/kubernetes-network-emulation-on-openshift
https://www.claise.be/yang-push-apache-kafka-semantic-network-visibility-for-analytics/
https://www.ansible.com/blog/addressing-netops-issues-with-event-driven-ansible

