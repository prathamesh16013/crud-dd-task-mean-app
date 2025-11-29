# MEAN CRUD App Deployment Assignment

A simple **MEAN stack CRUD application** deployed using Docker, Docker Compose, and automated CI/CD with Jenkins. Nginx is used as a reverse proxy, and MongoDB serves as the database.

## **Project Structure**

crud-dd-mean-app/
│
├─ backend/ # Node.js + Express backend
│ ├─ Dockerfile
│ ├─ package.json
│ ├─ server.js
│ └─ ...
│
├─ frontend/ # Angular frontend
│ ├─ Dockerfile
│ ├─ package.json
│ ├─ angular.json
│ └─ src/
│
├─ docker-compose.yml
├─ Jenkinsfile
└─ README.md

### **1. Clone the Repository**
```bash
git clone https://github.com/<your-username>/crud-dd-mean-app.git
cd crud-dd-mean-app

2. Build Docker Images

docker build -t <dockerhub-username>/mean-app-be:latest ./backend
docker build -t <dockerhub-username>/mean-app-fe:latest ./frontend

3. Push Images to Docker Hub

docker login
docker push <dockerhub-username>/mean-app-be:latest
docker push <dockerhub-username>/mean-app-fe:latest

4. Deploy Using Docker Compose on Ubuntu VM
ssh ubuntu@<vm-ip>
cd /path/to/deployment
docker-compose up -d --build

5. Access the Application
Open a browser and go to:
http://<public-ip>:8081

CI/CD Pipeline (Jenkins)

Pipeline Steps:

Checkout code from GitHub
Build Docker images for frontend and backend
Push images to Docker Hub
Deploy latest images on VM using Docker Compose
Jenkinsfile is included in the repository.

* Nginx Reverse Proxy Setup
Configured inside the frontend Docker image.
Serves Angular app on port 80.
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(3).png?raw=true)
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(1).png?raw=true)
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(1).png?raw=true)

Database:

MongoDB used as the database.
Can be deployed either:
Directly on Ubuntu VM
Via official MongoDB Docker image (included in docker-compose.yml)

![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(4).png?raw=true)
