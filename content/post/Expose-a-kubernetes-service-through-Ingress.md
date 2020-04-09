---
title: "Expose a kubernetes service through Ingress"
date: 2020-04-06T23:25:03+05:30
publishdate: 2020-04-06
lastmod: 2020-04-06
draft: false
tags: [ingress, kubernetes]
---

Let's dive right into it.

## Terms

- **Ingress** is a kubernetes API object that defines rules to map incoming traffic to backend services.
- **Ingress controller** watches over ingress, reads the rules, and implements them by acting as a reverse proxy system.
- **Reverse Proxy system** is basically something that sits in front of services and queries them on the client's behalf.

## Creating a dummy Service

Create a `deployment.yaml` file with following content and execute it -

```yaml
#deployment.yaml

apiVersion: v1
kind: Service
metadata:
  name: helloworld
spec:
  selector:
    app: helloworld
  ports:
    - port: 80
      targetPort: 5678

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: helloworld
spec:
  selector:
    matchLabels:
      app: helloworld
  template:
    metadata:
      labels:
        app: helloworld
    spec:
      containers:
        - name: helloworld
          image: hashicorp/http-echo
          args:
            - "-text=Hi There!"
          resources:
            limits:
              memory: "128Mi"
              cpu: "500m"
          ports:
            - containerPort: 5678
```

Output:

```
service/helloworld created
deployment.apps/helloworld created
```

## A little Theory before moving on to practical

The next part can be a little confusing so better I explain how things are gonna work.

{{< mermaid >}}

It’s important to understand the use of the ingress-controller here. What’s happening is that the user will hit ingress-controller (through some client like chrome or curl). Ingress-controller also keeps observing kubernetes Ingress resource all the time and therefore it knows all the ingress rules. Based on those rules, it will decide which service to fetch the data from and then returns it back to the client. This behavior is also known as reverse-proxying that-is retrieving resources on behalf of a client from one or more back-ends.

## Exposing the service through ingress

First we need to install nginx ingress controller. Instructions for that can be found [here](https://kubernetes.github.io/ingress-nginx/deploy/#using-helm).

Now do `kubectl get svc -n <ns>` where `ns` is the namespace where you have installed your nginx ingress controller. It will list out the services in that namespace. And you would see the nginx-ingress-controller service.

```bash
nginx-ingress-controller        LoadBalancer   10.0.85.102    23.101.65.225
nginx-ingress-default-backend   ClusterIP      10.0.123.59    <none>
```

We are only interested in the `nginx-ingress-controller` service right now. Notice that it is of type `LoadBalancer` which makes total sense because as I mentioned earlier a user should be able to hit ingress-controller from outside the cluster and that's possible only when the associated service is of type LoadBalancer.

Now, it's your task to get a name(DNS) for the external IP of `nginx-ingress-controller` which in my case is `23.101.65.225`. Getting a DNS is like not 100% necessary, you can simply hit the IP, but I would still suggest getting a DNS and you can some DNS'es for free on the internet. Now let's say you got a DNS name `www.goku.ez`.

Its time to create the ingress. Copy the below code in a YAML in your system and execute it with kubectl command.

```yaml
# ingress.yaml

apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: helloworld-ingress
spec:
  rules:
    - host: goku.ez
      http:
        paths:
          - path: /
            backend:
              serviceName: helloworld
              servicePort: 80
```
Output:
```
ingress.networking.k8s.io/helloworld-ingress created
```

what this rule says is - anyone coming to `goku.ez` at path `/` will be redirected to service `helloworld`. You can mention another path there like so:

```yaml
- path: /profile
  backend:
    serviceName: profileresolver
    servicePort: 80
```

and this would mean anyone visiting `goku.ez` at path `/profile` which is this URL `goku.ez/profile`, it will be redirected to `profileresolver` service.

Head over to goku.ez and see ingress doing magic for you.
