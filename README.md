# Kubernetes Workshop

[Presentation](https://docs.google.com/presentation/d/1BuB8xiFdeyI5P2Ah3rxulteG23i89daxX5UTyOgWq8Y/edit?usp=sharing)

## 🚧 

Docker images to use
- Webapp
    - ydata/docker-workshop:1.0
    - ghcr.io/ydataai/docker-workshop:1.0
- Redis
    - bitnami/redis:7.0.11
    - or another from dockerhub

### The deployment.yml file

#### Complete the file

Add a container with `webapp` using one of the docker images mentioned above

You have to set the image, the tag and expose the port 8000

Add another container with the `redis` image using the image above or other from the dockerhub (make sure you read how to use it)

Note the labels in the `template` and `selector` sections

#### Into the cluster

```bash
kubectl apply -f deployment.yml
```

Check the deployment in the cluster

```bash
kubectl get deployment -n <your_namespace_previously_created>
```

Check the pods (remember, which deployment has one or more pods, depending on the replicas property)

```bash
kubectl get pods -n <your_namespace_previously_created>
```

NOTE: You don't need the `-n <some_name_without_spaces>` if you have used kubens to set the default namespace

### The service.yml file

#### Complete the file

Add the necessary ports to expose the services in the deployment.

Note the selector, this needs to match the same labels in the deployment

#### Into the cluster

Apply the file to create the resources in the cluster

```bash
kubectl apply -f service.yml
```

Check the service created

```bash
kubectl get service -n <your_namespace_previously_created>
```

Let's access the service in the cluster. In order to achieve that, we have to a do a port-forward, which is like open a tunnel from our computer to the cluster.

```bash
kubectl port-forward svc/webapp -n <your_namespace_previously_created> 8080:8080
```

NOTE: You don't need the `-n <some_name_without_spaces>` if you have used kubens to set the default namespace