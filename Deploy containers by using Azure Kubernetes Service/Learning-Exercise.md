# Deploy containers by using Azure Kubernetes Service

## Tasks performed
- Deploy an AKS cluster
- Deploy and use Azure Container Registry
- Configure an AKS cluster
- Deploy applications to AKS
- Configure scaling in AKS

## Topics:
- Provisioning Azure Container Registry (ACR) and Azure Kubernetes Service (AKS).
- Building a Linux and Windows container images and store them in Azure Container Registry.
- Deploying container images to Azure Kubernetes Service. By the end of this guided exercise, you gain hands-on experience in creating and configuring these services in Azure.

![](./Screenshot%202024-02-07%20133257.png)

You will add a Windows node pool to the cluster. This required changing the network configuration to Azure CNI from the default Kubenet. The Kubenet network configuration does not support Windows node pools.

On the Networking tab of the Create Kubernetes cluster page, select the Azure CNI option,, select the Bring your own virtual network checkbox, in the Virtual network dropdown list, select vnet-01, and below the Cluster subnet textbox, select Managed subnet configuration.
On the vnet-01 | Subnets page, select + Subnet.
On the Add subnets page, specify the following settings and select Save:

Server image example
```javascript
const http = require('http')
const port = 80
const server = http.createServer((request, response) => {
  response.writeHead(200, {'Content-Type': 'text/plain'})
  response.write('Hello World from Node\n')
  response.end('Version: ' + process.env.NODE_VERSION + '\n')
})
server.listen(port)
console.log(`Server running at http://localhost: ${port}`)
```

package.json
```json
{
  "name": "helloworld",
  "version": "1.0.0",
  "description": "Sample app for ACR Build",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node server.js"
  },
  "license": "MIT"
}
```

Dockerfile
```dockerfile
FROM node:20.2-alpine
COPY . /src
RUN cd /src && npm install
EXPOSE 80
CMD ["node", "/src/server.js"]
```

Kubernetes Deployment Yaml file:

aka-deployment-l01.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hellofromnode-deployment
  labels:
    environment: dev
    app: hellofromnode
spec:
  replicas: 1
  template:
    metadata:
      name: hellofromnode
      labels:
        app: hellofromnode
    spec:
      nodeSelector:
        "kubernetes.io/os": linux
      containers:
      - name: hellofromnode
        image: ACR_NAME.azurecr.io/hellofromnode:v1.0
        resources:
          limits:
            cpu: 1
            memory: 800M
        ports:
          - containerPort: 80
  selector:
    matchLabels:
      app: hellofromnode
---
apiVersion: v1
kind: Service
metadata:
  name: hellofromnode-service
spec:
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 80
  selector:
    app: hellofromnode
```

kubectl get deployments -n=dev-node
kubectl get deployments -n=dev-dotnet

kubectl get services -n=dev-node
kubectl get services -n=dev-dotnet

az resource list --resource-group 'acr-01-RG' --query "[].name" --output tsv
az resource list --resource-group 'aks-01-RG' --query "[].name" --output tsv
