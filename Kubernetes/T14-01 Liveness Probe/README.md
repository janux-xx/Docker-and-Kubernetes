# L14-02 The Liveness Probe + Readiness Probe + Startup Probe

[More info...](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/)

## Liveness probe
Liveness probes determine when to restart a container. For example, liveness probes could catch a deadlock when an application is running but unable to make progress.

If a container fails its liveness probe repeatedly, the kubelet restarts the container.

Liveness probes do not wait for readiness probes to succeed. If you want to wait before executing a liveness probe, you can either define initialDelaySeconds or use a startup probe.

## Readiness probe
Readiness probes determine when a container is ready to start accepting traffic. This is useful when waiting for an application to perform time-consuming initial tasks, such as establishing network connections, loading files, and warming caches.

If the readiness probe returns a failed state, Kubernetes removes the pod from all matching service endpoints.

Readiness probes run on the container during its whole lifecycle.

## Startup probe
A startup probe verifies whether the application within a container is started. This can be used to adopt liveness checks on slow starting containers, avoiding them getting killed by the kubelet before they are up and running.

If such a probe is configured, it disables liveness and readiness checks until it succeeds.

This type of probe is only executed at startup, unlike liveness and readiness probes, which are run periodically.

>Much more in: [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)


## Deploy the pod

    kubectl apply -f pod.yaml

## Look at the pod events

    kubectl describe pod liveness-example

## Cleanup

    kubectl delete -f pod.yaml --force --grace-period=0


When the container starts, it executes this command:
```bash
/bin/sh -c "touch /tmp/healthy; sleep 15; rm -f /tmp/healthy; sleep 600"
```
For the first 30 seconds of the container's life, there is a ```sh /tmp/healthy``` file. So during the first 15 seconds, the command ```sh cat /tmp/healthy``` returns a success code. After 15 seconds, ```sh cat /tmp/healthy``` returns a failure code.

You can execute this to monitor over and over:
```sh
kubectl describe pod liveness-example
```


