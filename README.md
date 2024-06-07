# argo-workflows

Kubernetes-native workflow engine supporting DAG and step-based workflows.

### Install argo-workflows with helm

```bash
helm install argo-workflows argo/argo-workflows \
--create-namespace --namespace argo \
--set crds.install=false
```

### Apply RBAC and Create Secret

```bash
kubectl apply -k .
```

### Expose token

```bash
ARGO_TOKEN="Bearer $(kubectl get secret argo-service-account -o=jsonpath='{.data.token}' | base64 --decode)"
```

### Verify roles

```bash
kubectl auth can-i create pods --as=system:serviceaccount:argo:argo-service-account
kubectl auth can-i list deployments --as=system:serviceaccount:argo:argo-service-account
```

### Create ingress

```bash
kubectl apply -f ingress.yaml
```
