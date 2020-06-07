
# [Kubernetes](./index)

## ConfigMap

### Creating ConfigMap

#### Using yaml file (Sourcing key/value pairs)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config-map
data:
  key1: value1
  key22: value22
```

#### Using yaml file (Sourcing file)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: config-map-data-from-file
data:
  ui.properties: |
   color.good=purple
   color.bad=yellow
   allow.textmode=true
   how.nice.to.look=fairlyNice
 game.properties: |
   enemies=aliens
   lives=3
   enemies.cheat=true
   enemies.cheat.level=noGoodRotten
   secret.code.passphrase=UUDDLRLRBABAS
   secret.code.allowed=true
   secret.code.lives=30
```

#### Using command (Sourcing file)

```bash
kubectl create configmap configmap-command --from-file=game.properties --from-file=ui.properties
```

### POD Usages 

#### Using without Volume (Specific keys)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-config-map-pod
spec:
  containers:
  - name: busybox
    image: busybox
    command:
    - sh
    - -c
    - echo $(MY_VAR) && sleep 3600
    env:
    - name: MY_VAR
      valueFrom:
        configMapKeyRef:
          name: my-config-map
          key: key1
 ```

#### Using with Volume (Mounting all files)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-all-config
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: config-map-data-from-file
```

#### Using with Volume (Mounting specific file)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod-single-config
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config/ui.properties
  volumes:
  - name: config-volume
    configMap:
      name: config-map-data-from-file
```
