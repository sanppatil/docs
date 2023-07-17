
# [Kubernetes](../index)

## Multi-Container PODs

### How containers can interact with one another?

#### Shared Network

- Containers can access any listening ports on containers within the same pod, even if those ports are not exposed outside the pod.

- Each Pod is assigned a unique IP address for each address family.

- Every container in a Pod shares the network namespace, including the IP address and network ports. Containers inside a Pod can communicate with one another using localhost

##### Example - Container communicating with "Shared Network"

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: web-server
    image: nginx
    ports:
    - containerPort: 80
  - name: web-client
    image: radial/busyboxplus:curl
    command:
    - sh 
    - -c
    - curl localhost:80 && sleep 3600
 ```

#### Shared Storage Volume

- Containers in the same pod can be given the same mounted storage volumes, which allows them to interact with the same files.

##### Example - Container communicating with "Shared Volume"

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: two-container-pod
spec:
  volumes:
  - name: shared-data
    emptyDir: {}
  containers:
  - name: nginx-container
    image: nginx
    volumeMounts:
    - name: shared-data
      mountPath: /usr/share/nginx/html
  - name: debian-container
    image: debian
    command: ["/bin/sh"]
    args: ["-c", "echo Hello from the debian container > /pod-data/index.html"]
    volumeMounts:
    - name: shared-data
      mountPath: /pod-data
 ```

#### Shared Process Namespace

- ProcessnamespacesharingcanbeenabledbysettingshareProcessNamespace true in the pod spec. This allows containers within the pod to interact with, and signal, one another’s processes.

## Container Orchstration Patterns

### [Adapter Pattern](./AdapterPattern)

### [Ambassador Pattern](./AmbassadorPattern)

### [Sidecar Pattern](./SidecarPattern)

[back](./)