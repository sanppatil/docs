
# [Kubernetes](./index)

## SecurityContext & ServiceAccount

### Important Points

1. ServiceAccounts are used for allowing pods to interact with the Kubernetes API, and for controlling what those pods have access to do using the API.

2. By default, If SecurityContext is not provided in POD specs, then processes will with root credentials

3. SecurityContext and ServiceAccounts setup is at POD specs.

### SecurityContext Example

```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: my-security-context 
spec:
  securityContext:
    runAsUser: 2001
    fsGroup: 3001
  containers:
  - name: my-security-context-container
    image: busybox
    command: 
    - sh
    - -c
    - cat /message/message.txt && sleep 3600
    volumeMounts:
      - name: message-volume
        mountPath: /message
  volumes:
    - name: message-volume
      hostPath:
        path: /etc/message 
 ```

### ServiceAccount Example

#### Create ServiceAcccount

```bash
kubectl create serviceaccount user01
```

#### POD using ServiceAcccount

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-service-account-pod
spec:
  serviceAccountName: user01
  containers:
  - name: my-service-account-container
    image: busybox
    command:
    - sh 
    - -c
    - echo Hello World && sleep 3600
```

[back](./)