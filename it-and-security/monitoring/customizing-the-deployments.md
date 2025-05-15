# Customizing the deployments

## Editing the values file of kube-prometheus-stack

[The Values file provided on the repository](https://github.com/prometheus-community/helm-charts/blob/main/charts/kube-prometheus-stack/values.yaml), is around 3800 lines, so this section aims to sum up the parts needed to change on the values file before launching the deployment.

### Disabling alertmanager

Around line 144:

```yaml
alertmanager: false
```

### Grafana configuration

Enable Grafana, and make the storage persistent, by changing from this (Around line 754):

```yaml
grafana:
  enabled: true
  namespaceOverride: ""
```

To this

```yaml
grafana:
  enabled: true
  persistence:
    enabled: true
    type: pvc
    storageClassName: standard
    accessModes:
    - ReadWriteOnce
    size: 4Gi
    finalizers:
    - kubernetes.io/pvc-protection
  namespaceOverride: ""
```

Customize admin password, (around line 775-780):

```yaml
adminPassword: youradminpassword
```

Change grafana.ingress.enabled to true (around line 782):

```yaml
  ingress:
    ## If true, Grafana Ingress will be created
    ##
    enabled: true
```

Change grafana.ingress.hosts to your target URL, for example monitoring-vectice.my-company.com (around line 810):

```yaml
    hosts: 
      - monitoring-vectice.my-company.com
```

Change grafana.ingress.tls to the tls secret previously created, and add the host, for example monitoring-vectice.my-company.com (around line 810):

```yaml
    tls:
    - secretName: monitoring-tls
      hosts:
      - monitoring-vectice.my-company.com
```

Add json-exporter scrape job (around line 3000):

```yaml
    additionalScrapeConfigs:
    - job_name: 'backend-internal'
      scrape_interval: 60s
      scrape_timeout: 60s

      static_configs:
        - targets: ['json-exporter-prometheus-json-exporter:7979']
```
