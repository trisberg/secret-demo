# secret-demo

This is a demo app for testing Spring Boot's new `configtree` feature.

You need [Skaffold](https://skaffold.dev/docs/install/).

Build defaults to your user name as the Docker ID repo prefix.
If you want a different repo prefix change `$USER` to the one you prefer. 

To just build:

```
skaffold build --default-repo $USER
```

To create the Kubernetes secret which is mounted for the app:

```
kubectl create secret generic mysql \
  --from-literal=mysql-root-password=$(echo $RANDOM) \
  --from-literal=mysql-password=$(echo $RANDOM)
```

To deploy app to Kubernetes:

```
skaffold run --default-repo $USER --port-forward
```

> This will port forward to http://localhost:8080

To get the env:

```
curl -w'\n' localhost:8080/actuator/env
```

To clean up:

```
skaffold delete
kubectl delete secret mysql
```
