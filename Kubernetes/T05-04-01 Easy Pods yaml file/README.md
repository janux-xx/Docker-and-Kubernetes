# YAML - Simple structure to create a Pod

## Simple
```
apiVersion: v1
kind: Pod

metadata:
  name:  my-ngnix

spec:
  containers:
  - name:  my-nginx
    image:  janux666/ngnix:v1
    
```
> Let's run it in testing mode !

```
kubectl create -f easy.pod.yaml --dry-run=client --validate=true
```

Now you can run it ! !

```
kubectl create -f easy.pod.yaml
```