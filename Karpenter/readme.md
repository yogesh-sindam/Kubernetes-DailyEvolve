

**What | Why | How** 

Karpenter is a open source project, that scale the node depend on the workload requirement and provision the nodes.

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
this will be exatly match with node taint, then the pod will `schedule`, otherwise it will in `pending` state

if this node not present karpenter provision the node to match the requirement, before you have to mention it in nodepool.yaml


### Benefits of this architecture 
1. resource optimization
   - Right-sized instance for each workload
   - application use high CPU instance(c7i.xlarge)
   - monitoring use balanced instnace (m5a.large)
   - also on
2. cost Efficiency
   - node only create for each workload type
   - Auto-termination when pod is not running
   - different instance size for different needs(env, team,)

3. performance isolate
   - no resources are contention btw workload type
   - predictable performace
4. security
   - network and resource isolation between workload categoris
   - dedicated node for sensiive workloads(critical resource will be run)


# The Complete Flow
1. pod deployment -> appliaction has specific tolaration
2. scheduling     -> kubernetes try to schedule on existing and selected node
3. no matching node -> pods remain pending state
4. karpenter detection -> see pending pods with specific tolaration
5. node creation -> create a node with matching taints
6. pod scheduling -> pod schedules on newly provisioned node
7. Auto scaling -> node scales based on workload demand

## This is highly sophisticated multi-tenent architecture where karpenter acts as an intelligent provisioner, creating the right type of nodes for the right type of workloads, ensuring the perfect isolation and resource optimization.




