# Imperative kubectl Commands

## Pods

1. **Create Pod:** 
    kubectl run <pod-name> --image=<image-name>

2. **List Pods:** 
    kubectl get pods

3. **Describe Pod:** 
    kubectl describe pod <pod-name>

4. **Delete Pod:** 
    kubectl delete pod <pod-name>

5. **View Pod Logs:** 
    kubectl logs <pod-name>

6. **View Logs of a specific container in a Pod:**
    kubectl logs <pod-name> -c <container-name>

7. **Tail Logs (stream):**
    kubectl logs -f <pod-name>

8. **Exec into Pod (interactive shell):**
    kubectl exec -it <pod-name> -- /bin/

9. **Exec into Pod with specific container:**
    kubectl exec -it <pod-name> -c <container-name> -- /bin/

10. **Get Pod with label selector:**
    kubectl get pods -l <label-selector>

11. **Get Pod in specific namespace:**
    kubectl get pods -n <namespace-name>

12. **Delete Pod with label selector:**
    kubectl delete pods -l <label-selector>

## ReplicaSets

1. **Create ReplicaSet:**
    kubectl create replicaset <replicaset-name> --image=<image-name> --replicas=<number-of-replicas>

2. **List ReplicaSets:**
    kubectl get replicasets

3. **Describe ReplicaSet:**
    kubectl describe replicaset <replicaset-name>

4. **Delete ReplicaSet:**
    kubectl delete replicaset <replicaset-name>

5. **Get ReplicaSet in specific namespace:**
    kubectl get replicasets -n <namespace-name>

6. **Scale ReplicaSet:**
    kubectl scale replicaset <replicaset-name> --replicas=<number-of-replicas>

7. **Check status of ReplicaSet:**
    kubectl rollout status replicaset <replicaset-name>

8. **Pause ReplicaSet rollout:**
    kubectl rollout pause replicaset <replicaset-name>

9. **Resume ReplicaSet rollout:**
    kubectl rollout resume replicaset <replicaset-name>

## Deployments

1. **Create Deployment:**
    kubectl create deployment <deployment-name> --image=<image-name>

2. **List Deployments:**
    kubectl get deployments

3. **Describe Deployment:**
    kubectl describe deployment <deployment-name>

4. **Scale Deployment:**
    kubectl scale deployment <deployment-name> --replicas=<number-of-replicas>

5. **Update Deployment Image:**
    kubectl set image deployment/<deployment-name> <container-name>=<new-image>

6. **View Deployment rollout status:**
    kubectl rollout status deployment <deployment-name>

7. **Pause Deployment rollout:**
    kubectl rollout pause deployment <deployment-name>

8. **Resume Deployment rollout:**
    kubectl rollout resume deployment <deployment-name>

9. **Rollback Deployment to previous revision:**
    kubectl rollout undo deployment <deployment-name>

10. **Delete Deployment:**
    kubectl delete deployment <deployment-name>

11. **Get Deployment in specific namespace:**
    kubectl get deployments -n <namespace-name>

12. **Expose Deployment as a Service:**
    kubectl expose deployment <deployment-name> --type=<service-type> --port=<port> --target-port=<target-port>


## Namespaces

1. **Create Namespace:**
    kubectl create namespace <namespace-name>

2. **List Namespaces:**
    kubectl get namespaces

3. **Describe Namespace:**
    kubectl describe namespace <namespace-name>

4. **Delete Namespace:**
    kubectl delete namespace <namespace-name>

5. **Set a default namespace for the current context:**
    kubectl config set-context --current --namespace=<namespace-name>

6. **Get Resources in a Namespace:**
    kubectl get all -n <namespace-name>

7. **Delete Resources in a Namespace:**
    kubectl delete all --all -n <namespace-name>

8. **Get all Namespaces with labels:**
    kubectl get namespaces --show-labels


## Kubernetes Object Aliases

### Pods
- **Pod:** `po`
- **Pods:** `pods`
  
### ReplicaSets
- **ReplicaSet:** `rs`
- **ReplicaSets:** `replicasets`

### Deployments
- **Deployment:** `deploy`
- **Deployments:** `deployments`

### Namespaces
- **Namespace:** `ns`
- **Namespaces:** `namespaces`

### Services
- **Service:** `svc`
- **Services:** `services`

### ConfigMaps
- **ConfigMap:** `cm`
- **ConfigMaps:** `configmaps`

### Secrets
- **Secret:** `secret`
- **Secrets:** `secrets`

### ReplicationControllers
- **ReplicationController:** `rc`
- **ReplicationControllers:** `replicationcontrollers`

### StatefulSets
- **StatefulSet:** `sts`
- **StatefulSets:** `statefulsets`

### DaemonSets
- **DaemonSet:** `ds`
- **DaemonSets:** `daemonsets`

### Jobs
- **Job:** `job`
- **Jobs:** `jobs`

### CronJobs
- **CronJob:** `cj`
- **CronJobs:** `cronjobs`

### PersistentVolumeClaims
- **PersistentVolumeClaim:** `pvc`
- **PersistentVolumeClaims:** `persistentvolumeclaims`

### PersistentVolumes
- **PersistentVolume:** `pv`
- **PersistentVolumes:** `persistentvolumes`

### Ingresses
- **Ingress:** `ing`
- **Ingresses:** `ingresses`

### NetworkPolicies
- **NetworkPolicy:** `netpol`
- **NetworkPolicies:** `networkpolicies`

### LimitRanges
- **LimitRange:** `limits`
- **LimitRanges:** `limitranges`

### ResourceQuotas
- **ResourceQuota:** `quota`
- **ResourceQuotas:** `resourcequotas`

### ServiceAccounts
- **ServiceAccount:** `sa`
- **ServiceAccounts:** `serviceaccounts`

### Roles
- **Role:** `role`
- **Roles:** `roles`
