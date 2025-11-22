🧩 Kubernetes Deployment, Scaling, Exposing & Accessing in Minikube (Step-by-Step With Explanation)
Below is the full workflow you performed in the uploaded image — each command + what it does + why we use it.
________________________________________
1️⃣ Create a Deployment
Command
kubectl create deployment mynginx --image=nginx
What it Does
This creates a Kubernetes Deployment named mynginx using the official nginx container image.
Why We Need It
A Deployment ensures:
•	Pods are running
•	If a pod crashes, Kubernetes auto-restarts it
•	You can scale pods easily
________________________________________
2️⃣ Check Deployment Status
Command
kubectl get deployments
What it Does
Shows:
•	How many pods are running
•	If Deployment is healthy
•	READY / AVAILABLE pods
Why
To confirm the Deployment was successfully created and that pods have started.
________________________________________
3️⃣ Expose the Deployment as a NodePort Service
Command
kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80
What it Does
Creates a Service that exposes the Nginx app on a random NodePort (30000–32767).
Why
Without a service, the pods are internal and cannot be accessed from outside the cluster.
________________________________________
4️⃣ Scale the Deployment
Command
kubectl scale deployment mynginx --replicas=4
What it Does
Creates 4 pod replicas for the mynginx deployment.
Why
Scaling ensures:
•	Load balancing across multiple pods
•	High availability
•	Testing horizontal scaling
________________________________________
5️⃣ Check All Pods
Command
kubectl get pods
What it Does
Shows each individual pod:
•	Pod name
•	Status (Running / Error)
•	Restart count
•	Age
Why
To verify all 4 replicas are running fine.
________________________________________
6️⃣ Port-Forward the Service (Local Access)
Command
kubectl port-forward svc/mynginx 8082:80
What it Does
Maps:
•	Local machine port 8082
•	→ to service port 80
So opening http://localhost:8082 shows Nginx.
Why
Useful when:
•	NodePort is blocked
•	You want direct local access
•	Testing service without exposing publicly
________________________________________
7️⃣ Delete the Deployment
Command
kubectl delete deployment mynginx
What it Does
Deletes the Deployment → Deletes all pods it controls.
Why
Used during cleanup or when re-deploying new versions.
________________________________________
8️⃣ Access Minikube Dashboard
Command
minikube dashboard
What it Does
Opens Kubernetes Dashboard UI in browser.
Why
•	Visual monitoring of pods, services, deployments
•	Easy debugging
•	Real-time metrics
________________________________________
9️⃣ Stop Minikube
Command
minikube stop
What it Does
Stops the Minikube Kubernetes cluster.
Why
•	Saves CPU/RAM
•	Saves battery
•	Safe shutdown of cluster
________________________________________
✅ Final Summary Table
Step	Command	Why It’s Needed
Create Deployment	kubectl create deployment	Start app inside Kubernetes
Check Deployment	kubectl get deployments	Verify app is running
Expose Service	kubectl expose deployment	Allow external access
Scale Pods	kubectl scale	Increase replicas
Check Pods	kubectl get pods	Confirm healthy pods
Port Forward	kubectl port-forward	Access app locally without NodePort
Delete Deployment	kubectl delete deployment	Cleanup
Open Dashboard	minikube dashboard	GUI view of cluster
Stop Cluster	minikube stop	Free system resources
Deploy Maven Java Web App on AWS EC2 using Docker + Tomcat
________________________________________
✅ 1. Connect to EC2 Instance
On Windows CMD/PowerShell:
cd C:\Users\Lenovo\Desktop\AWS
ssh -i "keypair.pem" ubuntu@<EC2-PUBLIC-DNS>
Example:
ssh -i "keypair.pem" ubuntu@ec2-34-204-0-190.compute-1.amazonaws.com
________________________________________
✅ 2. Update System Packages
sudo apt update
sudo apt upgrade -y
________________________________________
✅ 3. Install Required Tools
Install Docker:
sudo apt install docker.io -y
Install Git:
sudo apt install git -y
Install Maven:
sudo apt install maven -y
Install Nano (optional):
sudo apt install nano -y
________________________________________
✅ 4. Clone the Project
git clone https://github.com/budarajumadhurika/SampleMavenWebProject.git
Move into folder:
cd SampleMavenWebProject
________________________________________
✅ 5. Build the Maven Project
mvn clean package
Verify WAR file:
ls target
Output should contain:
SampleMavenWebProject.war
________________________________________
✅ 6. Create Dockerfile
Create file:
nano Dockerfile
Paste this exactly:
FROM tomcat:9-jdk11
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

For normal html file:
FROM nginx:alpine
COPY . /usr/share/nginx/html
Save:
•	CTRL + O → Enter
•	CTRL + X
________________________________________
✅ 7. Build Docker Image
sudo docker build -t mywebserver .
________________________________________
✅ 8. Run Docker Container
sudo docker run -d -p 8080:8080 mywebserver
________________________________________
✅ 9. Verify Container
sudo docker ps
________________________________________
✅ 10. Access Web App in Browser
Open:
http://<EC2-PUBLIC-IP>:8080/
http://<EC2-PUBLIC-IP>:8080/projectname----use in nrml html

Example:
http://34.204.0.190:8080/
Your Java Maven Web App should now load successfully.
		



