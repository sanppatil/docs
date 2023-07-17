
# [Kubernetes](./index)

## Resources

### Important Points

- Resources are specified at container level

- **Resource Requests** -> The amount of resources a container needs to run Kubernetes uses these values to determine whether or a not a worker node has enough resources available to run a pod.
- **Resource Limits** -> The maximum resource usage of a container. The container run time will try to prevent the container from exceeding this amount of resource usage.
- Type of Resources
  - cpu
  - memory
  - ephemeral-storage

### Resources Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-resources-pod
spec:
  containers:
  - name: my-resources-container
    resources:
      requests:
        cpu: 250m
        memory: 64Mi
      limits:
        cpu: 500m
        memory: 128Mi
    image: busybox
    command:
    - sh
    - -c
    - echo Hello Kubernetes!! && sleep 3600
 ```
 [back](./)
