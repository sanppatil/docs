
# [Kubernetes](./index)

## Volumes

### emptyDir Volume

An emptyDir volume is first created when a Pod is assigned to a Node, and exists as long as that Pod is running on that node.

#### emptyDir Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: empty-dir-vol-pod
spec:
  volumes:
  - name: my-data-volume
    emptyDir: {}
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: my-data-volume
      mountPath: /tmp/data
```

### hostPath Volume

A hostPath volume mounts a file or directory from the host node’s filesystem into your Pod.

#### hostPath Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: host-path-vol-pod
spec:
  volumes:
  - name: system-data
    hostPath:
      path: /tmp/sample
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: system-data
      mountPath: /var/sys/sample
```
[back](./)