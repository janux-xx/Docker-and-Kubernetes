# T19-01 Developing at the Canary way

*This excercise will set a dev environment for testing.*

## In this case we are going yo create TWO ways to work with our development updates/upgrades:
1) Green / Blue deployments
2) [Canary deployments](https://kubernetes.io/docs/concepts/workloads/management/#canary-deployments)



### Task 1
Create a namespace called dev 
>If exist do not create it 
```sh
kubectl create ns dev
```

### Task 2

**IMPORTANT:** This task assumes that you have images named `ckad:stable` and `ckad:canary` available on your system. To create them, go to the `Canary/Build` folder and run `docker-compose build` to create the images.

change to dev context:
```
cd Build

kubectl config set-context --current --namespace=dev

docker-compose build
```
Your system has `ckad:stable` and `ckad:canary` images available and the current folder contains YAML files to be used to complete the task.

Are the images there?
```sh
docker images |grep ckad
```

1. Create resources in Kubernetes using the YAML files available in the current folder. List all the running Pods.

  ```
  cd ..
  kubectl create –f ./
  ```

2. Scale the `stable` Deployment to `6` replicas and the `canary` Deployment to `2` replicas.

  ```
kubectl scale deploy stable-deployment –-replicas=6
kubectl scale deploy canary-deployment --replicas=2
  ```

3. Modify the `canary` Deployment so that the Service will match it and direct traffic to the Pods.

  ```
  kubectl edit deploy canary-deployment
    # Add app: customer-app label into deployment template labels
  ```
4. Create a temporary Pod named `temp-pod` as an interactive TTY. Use the `alpine` image for the Pod and set `restart` to `Never`. 
```sh
# Get service cluster IP
kubectl get svc public-service

kubectl run -it --restart=Never --image=alpine temp-pod
```

5. Install `curl` into the `temp-pod` container using `apk add curl`, and run the following command until the output from a `canary` Pod is displayed: 

  ```sh 
  apk add curl
  curl <service-cluster-ip>
  ```
and see the magic inside the `temp-pod` or using `http://127.0.0.1` on your browser.

# Deleting all xD ...

```sh
kubectl delete deployments canary-deployment stable-deployment

kubectl delete svc public-service

kubectl delete pod temp-pod
```