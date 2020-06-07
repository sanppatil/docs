
# [Kubernetes](./index)

## PersistentVolumes & PersistentVolumeClaims

### PersistentVolume Example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: cust-pv
spec:
  storageClassName: local-storage
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 512Mi
  hostPath:
    path: /tmp/sample
```

### PersistentVolumeClaim Example

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: cust-pvc
spec:
  storageClassName: local-storage
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 128Mi
```

### POD Using PersistentVolume

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: cust-pod
spec:
  volumes:
  - name: data-vol
    persistentVolumeClaim:
      claimName: cust-pvc
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: data-vol
      mountPath: /var/cust
```
