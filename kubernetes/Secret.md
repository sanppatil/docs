
# [Kubernetes](./index)

## Secret

### Important Points

- The Secret contains two maps: data and stringData. The data field is used to store arbitrary data, encoded using base64. The stringData field is provided for convenience, and allows you to provide secret data as unencoded strings.

### Creating Secret

#### Using yaml file

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
stringData:
  myKey: myPassword
```

#### Using command (Sourcing Secret in commmand line)

```bash
kubectl create secret generic my-secret --from-literal=myKey=myPassword
```

#### Using command (Sourcing Secret in file)

```bash
kubectl create secret generic secret-config --from-file=password.txt
```

### POD Usages

#### Using without Volume (Specific secret)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-secret-pod
spec:
  containers:
  - name: my-app-container
    image: busybox  
    env:
    - name: MY_PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: myKey
    command:
    - sh 
    - -c
    - echo $(MY_PASSWORD) && sleep 3600
 ```

#### Using with Volume (Mounting specific file)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: vol-secret
spec: 
  containers:
  - image: busybox
    name: busybox
    command: ['sh', '-c', 'ls /etc/password;cat /etc/password/password.txt']
    volumeMounts:
    - name: secrete-volume
      mountPath: /etc/password
  volumes:
  - name: secrete-volume
    secret:
      secretName: secret-config
```
[back](./)