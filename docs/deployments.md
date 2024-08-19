# DEPLOYMENTS

You describe your desired state in a Deployment, and the Deployment Controller's job is to make the current state match the desired state. You declare your hopes and dreams, and it's Kubernetes' job to make them come true.

Remember when we had you delete a pod, only to see that a new pod was created in its place? It's kinda like chopping heads off of a hydra.

That's because the desired state described in our Deployment says we want 2 pods running at all times. When we delete one, the Deployment Controller sees that the current state doesn't match the desired state, so it creates a new pod to make them match again.

To look yaml file

`kubectl get deployment [PODNAME] -o yaml`

### [ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

Maintains a stable set of replica Pods running at any given time. It's the thing that makes sure that the number of Pods you want running is the same as the number of Pods that are actually running.

`kubectl get replicasets`

---

To create a yaml config file

`kubectl get deployment [PODNAME] -o yaml > web-deployment.yaml`

To apply the changes:

`kubectl apply -f web-deployment.yaml`

## Thrashing Pods

One of the most common problems you'll run into when working with Kubernetes is Pods that keep crashing and restarting. This is called "thrashing" and it's usually caused by one of a few things:

1. The application recently had a bug introduced in the latest image version
2. The application is misconfigured and can't start properly
3. A dependency of the application is misconfigured and the application can't start properly
4. The application is trying to use too much memory and is being killed by Kubernetes


## What is "CrashLoopBackoff"?
When a pod's status is CrashLoopBackoff, that means the container is crashing (the program is exiting with error code 1).

Because Kubernetes is all about building self-healing systems, it will automatically restart the container. However, each time it tries to restart the container, if it crashes again, it will wait longer and longer in between restarts. That's why it's called a "backoff".

## Config Maps

One way of set the env variables is the config maps.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: name
data:
  API_PORT: "8080"
```

`kubectl get configmaps`

To connect our deployment make sure apply it first.

Add the simple syntax to the containers section of deployment yaml:

```yaml
env:
  - name: API_PORT
    valueFrom:
      configMapKeyRef:
        name: name
        key: API_PORT
```

Then forward the port with 

`kubectl port-forward <pod-name> 8080:8080`

We can use this format to simplify

```yaml
envFrom:
  - configMapRef:
      name: name
```

### ConfigMaps are not secure

> ConfigMaps are a great way to manage innocent environment variables in Kubernetes. However, they are not cryptographically secure. ConfigMaps aren't encrypted, and they can be accessed by anyone with access to the cluster. If you need to store sensitive information, you should use Kubernetes Secrets or a third-party solution.


