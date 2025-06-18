# T18-01 Developing at the blue and Green way

*This excercise will set a dev environment for testing.*

## In this case we are going yo create TWO ways to work with our development updates/upgrades:
1) Green / Blue deployments
2) [Canary deployments](https://kubernetes.io/docs/concepts/workloads/management/#canary-deployments)



### Task 1
Create a namespace called dev
```sh
kubectl create ns dev
```

### Task 2

1. Create a Deployment named `nginx-deploy`. The Deployment should use the `nginx:stable-alpine` image and create `4` replicas, and use the new "dev" namespace.
```sh
kubectl config set-context --current --namespace=dev
```
```sh
kubectl create deployment nginx-deploy --image=nginx:stable-alpine --replicas=4 --port=80
```

2. Create a `NodePort` service named `nginx-svc` and associate it with the Pods created by the `nginx-deploy` Deployment. The service should expose port `9000` and a target port of 80.

```sh
kubectl expose deploy nginx-deploy --port=9000 --target-port=80 --type=NodePort --name=nginx-svc --type=LoadBalancer
```

3. Edit the `nginx-deploy` Deployment and change the number of replicas to `6`.
```
kubectl edit deploy/nginx-deploy
```

4. Ensure the service is associated with the `nginx-deploy` Pods by running the following command and checking that it returns HTML content. Replace `<node-port-value>` with the `nginx-svc` node port value.

```sh
kubectl get service nginx-svc

curl http://localhost:<node-port-value>
```
> Delete all !! :)
```sh
kubectl delete deplpoyment nginx-deploy

kubectl delete svc nginx-svc
```

### Task 3

**IMPORTANT:** This task assumes that you have images named `ckad:blue` and `ckad:green` available on your system. To create them, go to the `Blue-Green/Build` folder and run `docker-compose build` to create the images.

The current folder contains Kubernetes YAML files to create Blue/Green deployments and services. Images you'll use are also available on the system. View the files in the current folder using: `ls`

1. View the selectors in the `blue.svc.yml` and `green.svc.yml` files. Add a `role: blue` selector to `public.svc.yml`.

 ```
    code blue.svc.yml
    code green.svc.yml
    code public.svc.yml
  ```

2. Create the resources in Kubernetes using the YAML files available in the current folder. Run the following command to verify that the `blue` Pods are accessible using the public service. `curl localhost`

```
    kubectl config set-context --current --namespace=dev
    kubectl create -f ./

    curl localhost
  ```
  > You can try your browser to:
  ```
  http://127.0.0.1
  http://127.0.0.1:9000
  http://127.0.0.1:9001
```
and see whats going on.

3. Change the public service's `role` selector from `blue` to `green`. Run the following command to verify that the `green` Pods are accessible using the public service.    `curl localhost` or browser to: `http://127.0.0.1`

  ```sh
  kubectl set selector svc public-service "app=nginx,role=green"
  ```    
  ```
  curl localhost
  ```

  # Deleting all !!! xD

 ```sh
 kubectl delete deployment blue-deployment green-deployment
 
 kubectl delete svc blue-test-service green-test-service public-service
 ``` 
