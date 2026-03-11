How Developers Can Access the Cluster
🥇 If You Are Using Amazon EKS (Most Common Case)

In EKS, access is controlled via:

AWS IAM User / Role

aws-auth ConfigMap mapping

Kubernetes RBAC

*******************

Dev logs in to AWS (IAM User or Role)

Runs:

aws eks update-kubeconfig --region ap-south-1 --name dev-cluster

IAM identity gets mapped inside cluster

RBAC RoleBinding applies permissions

******************
```
kubectl edit configmap aws-auth -n kube-system
```
```
mapUsers: |
  - userarn: arn:aws:iam::123456789012:user/dev1
    username: dev1
    groups:
      - alpha-devs
```
```
```
kind: RoleBinding
metadata:
  name: alpha-devs-binding
  namespace: alpha
subjects:
- kind: Group
  name: alpha-devs
roleRef:
  kind: ClusterRole
  name: edit
  apiGroup: rbac.authorization.k8s.io
```
kubectl get pods -n alpha
kubectl delete pod xyz -n alpha
```