# Exp9-10
Experiment 10
1. Install Docker Desktop (Windows)  
2. Enable the Kubernetes option in Docker Desktop → Settings → Kubernetes → 
“Enable Kubernetes”. 
3. Verify installation: 
4. kubectl version --client 
5. kubectl get nodes 
✅ You should see a single node named docker-desktop.

Step 2: Create Deployment YAML File 
Create a new file deployment.yaml in VS Code: 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
name: my-web-app 
spec: 
replicas: 3 
selector: 
matchLabels: 
app: my-web-app 
template: 
metadata: 
labels: 
app: my-web-app 
spec: 
containers: - name: my-web-container 
image: nginx:latest 
ports: - containerPort: 80 

Step 3: Create Service YAML File 
Create service.yaml in the same directory: 
apiVersion: v1 
kind: Service 
metadata: 
name: my-web-service 
spec: 
selector: 
app: my-web-app 
type: NodePort 
ports: 
- protocol: TCP 
port: 80 
targetPort: 80 
nodePort: 30008

Step 4: Deploy the Application 
Apply both configuration files: 
kubectl apply -f deployment.yaml 
kubectl apply -f service.yaml 
Verify resources: 
kubectl get deployments 
kubectl get pods 
kubectl get services 

Step 5: Access the Application 
Get the service details: 
kubectl get svc 
Access your application using: 
http://localhost:30008 
You should see the default Nginx Welcome Page.

Step 6: Scale the Deployment 
To increase Pods from 3 → 5: 
kubectl scale deployment my-web-app --replicas=5 
kubectl get pods 
Observe that Kubernetes automatically starts 2 additional Pods.
