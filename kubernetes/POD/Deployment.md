
# [Kubernetes](../index)

## [Pod](./index)

### Deployment

#### Important Points

1. Defines a desired state for a set of replica pods, and works to maintain that state by creating, removing, and modifying those pods

2. While creating deployment, underlaying template schema exactly confirms to POD specs.

3. The deployment will manage all pods whose labels match this selector. When creating a deployment, make sure the selector matches the pods on the template!

#### Deployment Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      name: web-pod
      labels:
        app: web
    spec:
      containers:
      - name: web-container
        image: nginx
        ports:
        - containerPort: 8080
 ```

#### Kubectl commands for Rolling Updates/Rollbacks

##### Change deployment image

```console
kubectl set image deployments/web-deployment web-container=node --record
 ```

##### View deployment history

```console
kubectl rollout history deployments/web-deployment
```

##### Rollback deployment

```console
kubectl rollout undo deployments/web-deployment --to-revision=1
```

##### View deployment details for specific revision

```console
kubectl rollout history deployments/web-deployment --revision=2
```

##### Check deployment status

```console
kubectl rollout status deployments/candy-deployment
```
