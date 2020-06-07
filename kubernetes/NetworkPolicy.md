
# [Kubernetes](./index)

## Network Policy

### Type of selectors

- **podSelector** - selects particular Pods in the same namespace 
- **namespaceSelector** - selects particular namespaces for which all Pods
- **ipBlock** - selects particular IP CIDR ranges to allow as ingress sources or egress destinations

### Examples

#### Secure Web Server

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-server
  labels:
    app: secure
spec:
  containers:
  - name: web-server-cont
    image: nginx
    ports:
    - containerPort: 80
 ```

#### Web Client - Without Permission

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: web-client
  labels:
    allow-access: "no"
spec:
  containers:
  - name: web-client-cont
    image: radial/busyboxplus:curl
    command: ["/bin/sh", "-c", "while true; do sleep 3600; done"]
```

#### Network Policy (Canal plugin)

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy
spec:
  podSelector:
    matchLabels:
      app: secure
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          allow-access: "yes"
    ports:
    - protocol: TCP
      port: 80
  egress:
  - to:
    - podSelector:
        matchLabels:
          allow-access: "yes"
    ports:
    - protocol: TCP
      port: 80
```
