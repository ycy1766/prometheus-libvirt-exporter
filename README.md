# prometheus-libvirt-exporter

# Component
* helm chart for prometheus-libvirt-exporter (./)
* grafana dashboard (./grafana-dashboard/)

# Get started
### helm chart 

**prometheus-libvirt-exporter installation**
```
git clone https://github.com/ycy1766/prometheus-libvirt-exporter.git
cd prometheus-libvirt-exporter
# helm version 2
helm install --name prometheus-libvirt-exporter -f values.yaml .
# helm version 3
helm install prometheus-libvirt-exporter -f values.yaml .
```
> if you want to deploy exporter into specific nodes, you should modify nodeSelector.

**prometheus example configuration**
```     
# sample
     - job_name: prometheus-libvirt-exporter
       kubernetes_sd_configs:
       - role: endpoints 
       relabel_configs:
       - source_labels: ['__meta_kubernetes_pod_label_exporter']
         separator: ;
         regex: libvirt
         replacement: $1
         action: keep
```

**check label and set the nodeselector**
```
[root@deploy1 ~]# kubectl get nodes --show-labels
NAME        STATUS     ROLES    AGE   VERSION   LABELS
master1   Ready      master   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=master1,kubernetes.io/os=linux,node-exporter=enabled,node-role.kubernetes.io/master=,openstack-control-plane=enabled,openvswitch=enabled
master2   Ready      master   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=master2,kubernetes.io/os=linux,node-exporter=enabled,node-role.kubernetes.io/master=,openstack-control-plane=enabled,openvswitch=enabled
master3   Ready      master   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=master3,kubernetes.io/os=linux,node-exporter=enabled,node-role.kubernetes.io/master=,openstack-control-plane=enabled,openvswitch=enabled
worker1   Ready      <none>   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker1,kubernetes.io/os=linux,node-exporter=enabled,openstack-compute-node=enabled,openvswitch=enabled
worker2   Ready      <none>   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker2,kubernetes.io/os=linux,node-exporter=enabled,openstack-compute-node=enabled,openvswitch=enabled
worker3   NotReady   <none>   2d   v1.16.8   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,fluent-logging=enabled,kubernetes.io/arch=amd64,kubernetes.io/hostname=worker3,kubernetes.io/os=linux,node-exporter=enabled,openstack-compute-node=enabled,openvswitch=enabled
```

### grafana dashboard 
2 files in this repository.
- OpenStack Libvirt Dashboard.json (this dashboard has 'instance="$compute_node"')
- Libvirt Dashboard.json

These dashboard json file can be imported on Grafana.
