# T08-06 The job

*Jobs represent one-off tasks that run to completion and then stop.*

A Job creates one or more Pods and will continue to retry execution of the Pods until a specified number of them successfully terminate. 

- As pods successfully complete, the Job tracks the successful completions. 

- When a specified number of successful completions is reached, the task (ie, Job) is complete.

- Deleting a Job will clean up the Pods it created. 

- Suspending a Job will delete its active Pods until the Job is resumed again.

A simple case is to create one Job object in order to reliably run one Pod to completion. The Job object will start a new Pod if the first Pod fails or is deleted (for example due to a node hardware failure or a node reboot).

> You can also use a Job to run multiple Pods in parallel.


Let's now use the Job template.

## Create the Job

    kubectl apply -f job.yaml

## Get the jobs list

    kubectl get jobs

## Get more info

    kubectl describe job

## Get the pod name

Get the pod's log.  Something starting with **hello-**

    kubectl get pods

## Get the jobs list

Get the container's log.  You should see **Hello from the Job**.

    kubectl logs <podName>

## Cleanup

    kubectl delete -f job.yaml


[More info...](https://kubernetes.io/docs/concepts/workloads/controllers/job/)