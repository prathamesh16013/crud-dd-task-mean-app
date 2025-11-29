# MEAN CRUD App Deployment Assignment

MEAN stack CRUD application deployed using Docker, Docker Compose, and automated CI/CD with Jenkins. 
Nginx is used as a reverse proxy, and MongoDB serves as the database.

Presentation Layer (Frontend) - Handles the user interface.
Application Layer (Backend) - Contains business logic.
Data Layer (Database) - Stores and manages the application’s data.

Each layer will be deployed in a Docker container, and we use Jenkins to manage the CI/CD pipeline for the application.

Project Roadmap:

Tools Required:-
EC2: Set up a new Ubuntu virtual machine on any cloud platform on AWS.
Docker: To containerize the application components.
Docker Compose: To manage multi-container Docker applications.
Jenkins: For CI/CD automation.
Git: Version control.




 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(3).png?raw=true)
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(1).png?raw=true)
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(2).png?raw=true)
 ![Image Alt](https://github.com/prathamesh16013/crud-dd-task-mean-app/blob/master/Screenshot%20(4).png?raw=true)

Project Structure:

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

1. Clone the Repository
git clone https://github.com/prathamesh16013/crud-dd-mean-app.git
cd crud-dd-mean-app

2. Build Docker Images

docker build -t pratham16013/mean-app-be:latest ./backend
docker build -t pratham16013/mean-app-fe:latest ./frontend

3. Push Images to Docker Hub

docker login
docker push pratham16013/mean-app-be:latest
docker push pratham16013/mean-app-fe:latest

4. Deploy Using Docker Compose on Ubuntu VM
ssh ubuntu@<vm-ip>
cd /path/to/deployment
docker-compose up -d --build

5. Access the Application
Open a browser and go to:
http://<public-ip>:80

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


Database:

MongoDB used as the database.
Can be deployed either:
Directly on Ubuntu VM
Via official MongoDB Docker image (included in docker-compose.yml)
