
# [Kubernetes](./index)

## Services

### ClusterIP

Service is exposed within the cluster using its own IP address, and can be located via the cluster DNS using the service name.  This is default service type.

### Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: cluster-service
spec:
  type: ClusterIP
  selector:
    app: web
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

### NodePort

- Service is exposed externally on a listening port on each node in the cluster.
- When Service Type is NodePart, Usually, values of port and targetPort remains same.

### Example

```yaml
apiVersion: v1
kind: Service
metadata:
  name: node-service
spec:
  type: NodePort
  selector:
    app: web
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 32100
```

### LoadBalancer

Service is exposed via a load balancer created on a cloud platform.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: load-balancer-service
spec:
  selector:
    app: web
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
```

### ExternalName

Service does not proxy traffic to pods, but simply provides DNS lookup for an external address. This allows components within the cluster to lookup external resources in the same way they look up internal ones, through services.
