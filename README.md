# k8s-inspect-node-js
Primer ton how to test or profile code running in any environment (staging, production et al)



# list all pods
$ kubectl get po -n <name-space> -o wide

# Get the node process id
$ kubectl exec -it <pod-id-here> -n <name-space> -- /bin/sh -c "ps aux"

# Send node process signal to be inspectable
$ kubectl exec -it <pod-id-here> -n <name-space> -- /bin/sh -c "kill -USR1 <process-id-from-above>"

# port forward to pod to open websocket (bit finicky and requires re-trying)
$ kubectl port-forward <pod-id-here> -n <name-space> 9229:9229

# open a chrome browser and type the following
chrome://inspect

# Click on link to inpect process and hit record button profiler and wait 20 - 30 seconds and hit stop button after or
# View source and add debugger to debug code in real time to spot issues
