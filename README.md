# Kubernetes Kibana
 Deploy Kibana in Kubernetes

## Prerequisites

We should create a secret for basic auth

```shell
htpasswd -c ./auth kibana
```

Now we have a `auth` file for create our secret

```shell
kubectl create secret generic kibana-auth --from-file auth
```

## Install

* Install [Elasticsearch](https://github.com/hatamiarash7/Kubernetes-Elasticsearch)
* Create a `ConfigMap` for kibana's ENV. See [kibana.yml](https://github.com/elastic/kibana/blob/master/config/kibana.yml) for full list of options.

```shell
kubectl create -f configmap.yml
```

Create other parts :

```shell
kubectl create -f service.yml
kubectl create -f deployment.yml
```

Check kibana's Pod for logs and wait to see `green status`. Then you can deploy your ingress to access Kibana from browser :

```shell
kubectl create -f ingress.yml
```

You can access Kibana from `server.name` that defined in `configmap.yml`. Defult value is [http://kibana.local](http://kibana.local)
