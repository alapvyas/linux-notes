## Kubernates useful commands

```kubectl get nodes```

This is to get the number of nodes in the cluster

```kubectl get pod```

This is to get the pods in the cluster

```kubectl get service```

This is to get services in the cluster. 

```kubectl create deployment``` | ```kubectl get deployment```

In Kubernates, you don't (You can though!) create pods as pods are the smallest units of a Kubernates cluster.
You would instead create a deployment. 

```kubectl get replicaset```

It gets the replicasets created by the deployment. 

```kubectl create deployment nginx-depl --image=nginx```

Example of how to create a deployment

```kubectl edit deployment nginx-depl```

To edit the deployment. 

```kubectl logs <pod name>```

To check logs of the applications in the pod

```kubectl describe pod <pod name>```

To get a proper description of the pod. 

```kubectl exec -it <pod name> -- /bin/bash```

To exec into a pod. 

```kubectl delete deployments <name of deployment>```

To delete a deployment

```kubectl apply -f <nameofthefile.yaml>```

Instead of passing all arguments in a single command, its easier to configure deployments in a file in yaml and
then run the file instead. If any changes are required, you can always edit the file and run it again. Basically,
you can create and update deployments with this. 