# prometheus-libvirt-exporter

prometheus example configuration
```     
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