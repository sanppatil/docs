
# [Kubernetes](./index)

## Miscellaneous

### Interacting with Debian containers

#### Update container OS

```bash
apt-get update
 ```

#### Install curl command

```bash
apt-get install curl
 ```

### Useful Commands

#### Login into container shell

```bash
kubectl exec -it <<name-of-pod>> -- /bin/sh
 ```

### Important Pointers

- While creating Service, property name for selecting label is "selector" -> 

- While creating Deployment, property name for selecting label is,  "selector" -> "matchLabels"

- While creating NetworkPolicy, property name for selecting label is, "podSelector" -> "matchLabels"

[back](./)