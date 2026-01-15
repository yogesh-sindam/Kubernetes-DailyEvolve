`kubectl get ingress`

```
my-app-ingress          (stable)
my-app-ingress-canary   (created by Argo Rollouts)

```
```
annotations:
  nginx.ingress.kubernetes.io/canary: "true"
  nginx.ingress.kubernetes.io/canary-weight: "10"
backend:
  service:
    name: my-app-canary

```

intially you are telling all traffic means(100%) will sent to service in name:my-app-stable

when you enable then trafficrouting 
dynamically route the traffic to another service mention in `rollout.yaml` according to setWeight
