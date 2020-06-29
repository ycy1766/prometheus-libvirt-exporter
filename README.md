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

### grafana dashboard 
  2 files in this repository.
  - OpenStack Libvirt Dashboard.json (this dashboard has 'instance="$compute_node"')
  - Libvirt Dashboard.json
