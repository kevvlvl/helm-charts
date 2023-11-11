# Helm repository

The following repo is published as a helm repository using Github Pages at the following URL: https://kevvlvl.github.io/helm-charts/charts

## Add the helm repo
```
helm repo add mycharts https://kevvlvl.github.io/helm-charts/charts
```

## An example chart implementing the template chart

```
❯ cd ./src/helm-chart-webapp

❯ helm dependency build
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "mycharts" chart repository
Update Complete. ⎈Happy Helming!⎈
Saving 1 charts
Downloading helm-chart-common from repo https://kevvlvl.github.io/helm-charts/charts/
Deleting outdated charts

❯ helm template .
---
# Source: helm-chart-webapp/templates/configmap.yaml
apiVersion: v1
data:
  city: Montreal
  color: red
  env: prod
kind: ConfigMap
metadata:
  name: env
  namespace: app
---
# Source: helm-chart-webapp/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx
  name: nginx
  namespace: app
spec:
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: nginx
---
# Source: helm-chart-webapp/templates/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx
  name: nginx
  namespace: app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - image: nginxinc/nginx-unprivileged:1.25
        name: nginx
        ports:
        - containerPort: 8080
```

As we can see, our ConfigMap is there which is based off the configmap template
