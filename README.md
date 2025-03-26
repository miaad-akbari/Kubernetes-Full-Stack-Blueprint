# Kubernetes Full-Stack Blueprint

This project is a comprehensive collection of Kubernetes manifests and Helm charts designed to deploy a full-stack production-ready environment. It includes configurations for applications, databases, storage systems, monitoring, security, and CI/CD tools like ArgoCD.

## Project Structure
```
k8s/
│── base/ # Base configurations for all environments
│ │── namespace.yaml
│ │── ingress.yaml
│ │── network-policy.yaml
│
│── apps/ # Applications
│ │── backend/
│ │ │── deployment.yaml
│ │ │── service.yaml
│ │ │── hpa.yaml
│ │
│ │── frontend/
│ │ │── deployment.yaml
│ │ │── service.yaml
│ │ │── ingress.yaml
│
│── databases/ # Databases
│ │── postgresql/
| │── volume-storageclass/
| │ │── pvc.yaml
| │── volume-hostPath/
| | │── pv-pvc-hostpath.yaml
│ │ │── deployment.yaml
│ │ │── service.yaml
│ │ │── secret.yaml
│ │
│ │── mysql/
| │── volume-storageclass/
| │ │── pvc.yaml
| │── volume-hostPath/
| | │── pv-pvc-hostpath.yaml
│ │ │── deployment.yaml
│ │ │── service.yaml
│ │ │── secret.yaml
│ │
│ │── mongodb/
| │── volume-storageclass/
| │ │── pvc.yaml
| │── volume-hostPath/
| | │── pv-pvc-hostpath.yaml
│ │ │── statefulset.yaml
│ │ │── service.yaml
│ │
│ │── redis/
| │── volume-storageclass/
| │ │── pvc.yaml
| │── volume-hostPath/
| | │── pv-pvc-hostpath.yaml
│ │ │── deployment.yaml
│ │ │── service.yaml
│
│── storage/ # Storage systems
│ │── minio/
│ │ │── deployment.yaml
│ │ │── service.yaml
│ │ │── pvc.yaml
│ │
│ │── longhorn/
│ │ │── storage-class.yaml
│
│── monitoring/ # Monitoring
│ │── prometheus.yaml
│ │── grafana.yaml
│ │── loki.yaml
│ │── thanos.yaml
│
│── security/ # Security
│ │── vault.yaml
│ │── rbac.yaml
│ │── cert-manager.yaml
│
│── argocd/ # ArgoCD
│ │── applications.yaml
│ │── projects.yaml
│
│── kustomization.yaml # Kustomize for managing environments
│
│── helm/ (optional) # Helm Charts
│ │── myapp/
│ │ │── Chart.yaml
│ │ │── values.yaml
│ │ │── templates/
│ │ │ │── deployment.yaml
│ │ │ │── service.yaml

```

---

## How to Use

### 1. Clone the Repository
```
git clone https://github.com/miaad-akbari/Kubernetes-Full-Stack-Blueprint.git
```
```
cd kubernetes-full-stack-blueprint
```
## 2. Apply Manifests Using kubectl
You can apply the manifests individually or all at once using kustomize.

### Apply All Manifests
```
kubectl apply -k .
```
### Apply Individual Files
```
kubectl apply -f path/to/file.yaml
```
### Delete Resources
```
kubectl delete -f path/to/file.yaml
```
### Check Pods and Services
```
kubectl get pods -n production
kubectl get svc -n production
```
### Describe a Resource
```
kubectl describe pod <pod-name> -n production
```
### Logs from a Pod
```
kubectl logs <pod-name> -n production
```
## 3. Using Helm
If you want to use Helm for deploying applications, follow these steps:

#### Install Helm
```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```
### Install a Helm Chart
### Navigate to the helm/myapp directory and run:

```
helm install myapp .
```
#### Upgrade a Helm Release
```
helm upgrade --install myapp .
```
#### Uninstall a Helm Release

```
helm uninstall myapp
```
####  List Helm Releases
```
helm list
```
## 4. Using ArgoCD
If you're using ArgoCD for GitOps, you can deploy the applications and projects defined in the argocd/ directory.

### Apply ArgoCD Applications
```
kubectl apply -f argocd/applications.yaml
```
#### Apply ArgoCD Projects
```
kubectl apply -f argocd/projects.yaml
```
### Key Features
* Applications: Deploy backend and frontend applications with Horizontal Pod Autoscaling (HPA).

* Databases: Supports PostgreSQL, MySQL, MongoDB, and Redis with Persistent Volume Claims (PVC) and Secrets.

* Storage: Includes MinIO for object storage and Longhorn for distributed block storage.

* Monitoring: Comprehensive monitoring with Prometheus, Grafana, Loki, and Thanos.

* Security: Vault for secrets management, RBAC for access control, and Cert-Manager for TLS certificates.

* CI/CD: ArgoCD for GitOps and Helm for templating and deployment.
