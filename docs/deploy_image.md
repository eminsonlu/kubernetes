## Deploying an image

The `kubectl create deployment` command will create a "deployment" for us. We'll talk more about the nuances of "deployments" later. But to put it simply, we only need to provide two things:

1. The name of the deployment (this can be anything, it's used to identify the deployment)
2. The ID of the Docker image we want to deploy (it would be a full URL if we weren't hosting the image on Docker Hub, which is the default)

`kubectl create deployment [name] --image=[image_url]`

To make sure the deployment was successful, run:

`kubectl get deployments`

## Accessing the web page

By default, resources inside of Kubernetes run on a private, isolated network. They're visible to other resources within the cluster, but not to the outside world.

In order to access the application from your local network, you'll need to use kubectl to do some port forwarding. First, run:

`kubectl get pods`

You should see something like this:

|NAME                                   |READY|STATUS  |RESTARTS |AGE|
|---------------------------------------|-----|--------|---------|---|
|somepodname-web-679cbcc6cd-cq6vx       |1/1  |Running | 0       |20m|


`kubectl port-forward PODNAME 8080:8080`

then navigate the `https://localhost:8080`

