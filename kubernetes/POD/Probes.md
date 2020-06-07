
# Kubernetes

## [Pod](./index)

### Liveness Probe

> Determines whether the container is running properly - When a liveness probe fails, the container will be shut down or restarted, depending on its RestartPolicy.

#### Exec Probe - Sample

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: exec-liveness
spec:
  containers:
  - name: liveness
    image: busybox
    command:
    - /bin/sh
    - -c
    - touch /tmp/healthy; sleep 30; rm -rf /tmp/healthy; sleep 600
    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
 ```

#### Http Probe - Sample

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: http-liveness
spec:
  containers:
  - name: http-liveness
    image: k8s.gcr.io/liveness
    command:
    - /server
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
        httpHeaders:
        - name: Custom-Header
          value: Awesome
      periodSeconds: 3
      initialDelaySeconds: 3
 ```

#### TCP Probe - Sample

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: tcp-liveness
spec:
  containers:
  - name: goproxy
    image: k8s.gcr.io/goproxy:0.1
    ports:
    - containerPort: 8080
    readinessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
 ```

### Readiness Probe

> 	Determines whether the container is ready to serve requests - Requests will not be forwarded to the container until the readiness probe succeeds.

