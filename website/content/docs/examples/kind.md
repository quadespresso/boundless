---
title: "Kind Cluster"
draft: false
weight: 1
---

```yaml
apiVersion: boundless.mirantis.com/v1alpha1
kind: Blueprint
metadata:
  name: kind-cluster
spec:
  kubernetes:
    provider: kind
  components:
    core:
      ingress:
        enabled: true
        provider: ingress-nginx
        config:
          controller:
            service:
              nodePorts:
                http: 30000
                https: 30001
              type: NodePort
    addons:
      - name: example-server
        kind: chart
        enabled: true
        namespace: default
        chart:
          name: nginx
          repo: https://charts.bitnami.com/bitnami
          version: 15.1.1
          values: |
            "service":
              "type": "ClusterIP"

```
