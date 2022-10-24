## Logs from a specific pod
```bash
$ kubectl log <pod_name>
```

## Extract logs from all pods into a file
```bash
$ kubectl get pods --no-headers | awk '{ print $1 }' | xargs -I{} sh -c 'kubectl logs {} > log_{}.log'
```
