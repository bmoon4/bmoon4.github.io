# Kubernetes practice on GKE
This is my first GKE project.
URL: moondevops.com 

## Components 
The GKE cluster consists one loadbalancer and three pods. 
Each pod has seven containers including a Nginx server container delivering a static HTML page.  

## YAML 

```bash
apiVersion: extensions/v1beta1
kind: Deployment
metadata: 
  name: static-html-image
spec:
  replicas: 3
  selector:
    matchLabels:
      app: static-html-image
  template:
    metadata:
      labels:
        app: static-html-image
    spec:
      containers:
      - env:
        image: gcr.io/annular-fold-285623/static-html-image:v2
        imagePullPolicy: Always
        name: static-html-image
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: static-html-image
  name: static-html-image-service
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: static-html-image
  type: LoadBalancer


```