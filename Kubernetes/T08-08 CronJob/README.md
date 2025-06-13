# T08-08 The CronJob

*A CronJob starts one-time Jobs on a repeating schedule.*

- CronJob is meant for performing regular scheduled actions such as backups, report generation, and so on. 

- One CronJob object is like one line of a crontab (cron table) file on a Unix system. 

- It runs a Job periodically on a given schedule, written in Cron format.

> CronJobs have limitations and idiosyncrasies. For example, in certain circumstances, a single CronJob can create multiple concurrent Jobs.

Let's now use the CronJob template.

## Create the Job

    kubectl apply -f cronjob.yaml

## Get the jobs list

    kubectl get cronjobs

## Get more info

    kubectl describe cronjob

## Get the pod name

Get the pod's log.  Something starting with **hello-**

    kubectl get pods

## Get the jobs list

Get the container's log.  You should see **Hello from the Job**.

    kubectl logs <podName>

## Cleanup

    kubectl delete -f cronjob.yaml

[More info...](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)