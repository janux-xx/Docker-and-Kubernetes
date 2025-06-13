# Metrics Server

Is the Metrics Server installed in your cluster?  Look for a pod called **metrics-server** in the kube-system namespace

    kubectl get po -n kube-system 

If not, install the Metrics Server

    kubectl apply -f components.yaml

The YAML file was downloaded from the Metrics Server Git repo located here:

    https://github.com/kubernetes-sigs/metrics-server/releases

The file was edited to include an extra parameter in the args section of the Deployment

    - --kubelet-insecure-tls


Deleting the Metrics Server

```sh
kubectl delete -f components.yaml
```

[More info...](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/#metrics-server)