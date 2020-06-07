
# [Kubernetes](../index)

## Pod

### Pod with Container Port

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-container-port
spec:
  containers:
  - name: web-server
    image: nginx
    ports:
    - containerPort: 7777
 ```

### Pod with Commands and Args

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-command
spec:
  containers:
  - name: busybox
    image: busybox
    command:
    - echo
    args:
    - Hello World
    - How are you
  restartPolicy: Never
 ```

## [Deployment](./Deployment)

## [Probes](./Probes)
