## Deploying the Examples

To deploy these examples to a Kubernetes cluster, follow these steps for each manifest:

1. **For the Pod**:
   ```bash
   kubectl apply -f nginx-pod.yaml
   ```

2. **For the ReplicaSet**:
   ```bash
   kubectl delete pod -l app=nginx-hello-world  # Clean up the pod from step 1
   kubectl apply -f nginx-replicaset.yaml
   ```

3. **For the Deployment**:
   ```bash
   kubectl delete rs -l app=nginx-hello-world  # Clean up the ReplicaSet from step 2
   kubectl apply -f nginx-deployment.yaml
   ```
