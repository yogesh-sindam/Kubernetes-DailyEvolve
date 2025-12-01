

** what | Why | How ** 

Karpenter is a open source

### how pod will be scduled 
pod has tolation matching taint's `key, value, effect`

```
 tolerations:
  - key: "node-type"
    operator: "Equal"
    value: "application"
    effect: "NoSchedule"

 tolerations:
  - key: "node-type"
    operator: "Equal"
    value: "monitoring"
    effect: "NoSchedule"
```
this will be exatly match with node taint, then the pod will schedule,
if this node not present karpenter provision the node to match the requirement, before you have to mention it in nodepool.yaml


