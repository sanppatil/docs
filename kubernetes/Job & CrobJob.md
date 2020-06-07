
# [Kubernetes](./index)

## Job & CrobJob

### Important Points

1. Creates one or more pods to do work and ensures that they successfully finish.

2. backoffLimit - Specify the number of retries before considering a Job as failed. The back-off limit is set by default to 6. Failed Pods associated with the Job are recreated by the Job controller with an exponential back-off delay (10s, 20s, 40s …) capped at six minutes.

3. While creating deployment, underlaying template schema exactly confirms to POD yaml. Only a RestartPolicy equal to Never or OnFailure is allowed.

4. RestartPolicy is defined at POD level.

### Job Example

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: test-job
spec:
  template:
    metadata:
      name: test-pod
    spec:
      containers:
      - name: test-container
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
 ```

### CronJob Example

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: test-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    metadata:
      name: test-job
    spec:
      template:
        metadata:
          name: test-pod
        spec:
          containers:
          - name: test-container
            image: busybox
            command:
            - /bin/sh
            - -c
            - date; echo Hello from the Kubernetes cluster
          restartPolicy: OnFailure
```
