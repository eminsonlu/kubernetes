## PODS

> "Pods are the smallest deployable units of computing that you can create and manage in Kubernetes." *-- Kubernetes Team*

Simply a docker container for us.

Pods are die. Often.

- This because flexibility and resilience.If a Pod encounters a problem, it can be easily terminated and replaced with a new, healthy instance. This model not only allows for high availability but also promotes immutability. Instead of manually patching or updating existing environments, you spin up new versions of the entire environment.

- As a developer, it's crucial to understand that it's rarely a good idea to store persistent data on a Pod. 

---

#### Print the logs (what the container is printing to stdout) of your older pod:

`kubectl logs PODNAME`

---

#### Kill that older pod:

`kubectl delete pod PODNAME`

>When a pods is manually deleted a new pod is created from the same image (which kinda feels like a restart).

---

`kubectl get pods -o wide`

This will give you a wide information about pods

---

And a one command i didn't understand exactly why we need :D

`kubectl proxy`