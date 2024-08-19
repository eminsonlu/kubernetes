## Minikube

During this course, we'll be using [Minikube](https://minikube.sigs.k8s.io/docs/) to practice with Kubernetes. In production, you probably wouldn't use Minikube, you would use a cluster of servers, probably in the cloud. That's expensive! Minikube is a fantastic tool that allows you to run a single-node Kubernetes cluster on your local machine.

## Assignment
### Install

Follow the official [installation instructions for Minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fmacos%2Farm64%2Fstable%2Fbinary+download). Notice at the top the "what you'll need" section. If you don't have the system requirements, you'll have a hard time getting everything up and running, unfortunately.

## Verify installation

Run `minikube version` to verify that Minikube is installed correctly.

## Run Minikube

We'll be using Kubernetes with Docker, which is arguably the most common way to use Kubernetes. Make sure your Docker daemon is running before starting Minikube.

Next, run:

`minikube start`

You should see a message like "kubectl is now configured to use "minikube" cluster and "default" namespace by default".

## Dashboard

Next, run the following command:

`minikube dashboard --port=63840`

This will open a browser window with a locally hosted dashboard for your cluster. You can use this dashboard to view and manage your cluster. Port is just a reminder.

## Troubleshooting Tips

WSL Virtualization
You can have problems if virtualization is not enabled.

> Docker desktop Settings -> Resources -> WSL integration (Check the box to enable integration with default WSL distro)

## Previous minikube installations

If you've installed minikube in the past, you might have conflicts. If you don't care about your old minikube clusters, you can delete them by running:

`minikube stop`

`minikube delete`

Then restart minikube.