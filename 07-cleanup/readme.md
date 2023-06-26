# 🧹️ Cleanup

## Stop Minikube

If the `hello` command has stopped by now, and if you haven't started any other background jobs, you can terminate the minikube tunnel like so:
```bash
kill $! # Kill the most recent backgrounded job in this shell.
```

If `hello` hasn't terminated or there are any other jobs, you may need to kill them manually:
```bash
jobs
kill %<YOUR-JOB-NUMBER>
```

Terminate the Minikube cluster:
```bash
minikube delete -p kube-workshop
minikube profile minikube # Set the default profile back to the original default.
```

## 🗄️ Remove the Workshop Directory
```bash
popd
rm ~/kube-workshop/*.yaml
rmdir ~/kube-workshop
```


## Navigation

[Return to Main Index 🏠](../readme.md) ‖
[Previous Section ⏪](../06-autoscaler/readme.md)
