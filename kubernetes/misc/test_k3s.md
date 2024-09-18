
# Quick 'Hello World' HTTP deployment for testing K3s and Traefik

Basic 'Hello World' web page on my K3s cluster:

1. Create an HTML file to be stored as a ConfigMap:

```bash
cat <<EOT>> index.html
<html>
<head>
  <title>Hello World!</title>
</head>
<body>Hello World!</body>
</html>
EOT
```

2. Create a ConfigMap with the HTML from the file you just created:

`$ kubectl create configmap hello-world --from-file index.html`

3. Create the following Kubernetes resource definitions into a file named hello-world.yml:

```yaml
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: hello-world
  annotations:
    ingressClassName: "traefik"
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: hello-world
            port:
              number: 80

---
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  ports:
    - port: 80
      protocol: TCP
  selector:
    app:  hello-world

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world-nginx
spec:
  selector:
    matchLabels:
      app: hello-world
  replicas: 1
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
        volumeMounts:
        - name: hello-world-volume
          mountPath: /usr/share/nginx/html
      volumes:
      - name: hello-world-volume
        configMap:
          name: hello-world
```

4. Deploy the Nginx container deployment, Service, and Traefik Ingress resources with:


`$ kubectl apply -f hello-world.yml`

5. Expose the port by creating the cluster or modifying the cluster

```bash
# Modify Cluster
k3d cluster edit test --port-add "8080:80@loadbalancer"

# Create cluster
k3d cluster create test -p "8080:80@loadbalancer" --agents 2
```

After a few seconds, you should be able to access port 80 on any member nodes (assuming networking is working), and get back:

```bash
$ curl localhost:80
<html>
<head>
  <title>Hello World!</title>
</head>
<body>Hello World!</body>
</html>
```

And in my case, I could test out the external routing and make sure that same response was making it through. Yay!

Bibliography:
- https://www.jeffgeerling.com/blog/2022/quick-hello-world-http-deployment-testing-k3s-and-traefik
- https://rob-mengert.medium.com/understanding-k3d-ingress-b94697638f3b