# k8s-inspect-node-js
Primer on how to test or profile code running in any k8s environment (staging, production et al)

The benefit of this approach is to quickly test issues in staging or production narrowing down problem areas on hard to locally reproduce bugs or performance problems.


1. List all pods
```bash
$ kubectl get po -n <name-space> -o wide
```

2. Get the node process id
```bash
$ kubectl exec -it <pod-id-here> -n <name-space> -- /bin/sh -c "ps aux"
```

3. Send node process signal to be inspectable
```bash
$ kubectl exec -it <pod-id-here> -n <name-space> -- /bin/sh -c "kill -USR1 <process-id-from-above>"
```

4. port forward to pod to open websocket (bit finicky and requires re-trying)
```bash
$ kubectl port-forward <pod-id-here> -n <name-space> 9229:9229
```

5. open a chrome browser and type the following
```bash
chrome://inspect
```

- Click on link to inpect process and hit record button profiler and wait 20 - 30 seconds and hit stop button after or
- View source and add debugger to debug code in real time to spot issues
