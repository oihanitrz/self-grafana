# Self Grafana with Observatorium (RHACM)

RBAC example (on hub cluster:)

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
 name: open-cluster-management:viewer:dev-edc-admin
rules:
  - apiGroups:
      - "cluster.open-cluster-management.io"
    resources:
      - managedclusters # CLUSTER
    resourceNames: 
      - ocp4-virt
    verbs: 
      - metrics/open-cluster-management-addon-observability # NAMESPACE
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: open-cluster-management:viewer:dev-edc-admin
subjects:
- kind: Group
  apiGroup: rbac.authorization.k8s.io
  name: dev-edc-admin
roleRef:
  kind: ClusterRole
  name: open-cluster-management:viewer:dev-edc-admin
  apiGroup: rbac.authorization.k8s.io
```
Give to `dev-edc-admin` group access to `open-cluster-management-addon-observability` namespace metrics on `ocp4-virt` cluster.