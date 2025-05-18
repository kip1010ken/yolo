
 # 🐳 YOLO App - GKE Deployment
 
This guide explains how to deploy the YOLO application stack to a **Google Kubernetes Engine (GKE)** cluster. The app consists of:

- A **MongoDB** database (with persistent storage)
- A **Backend API**
- A **Frontend UI**

The application is exposed to the internet via a Kubernetes `LoadBalancer` service, accessible at:

🌐 **http://35.232.135.122**

---

## 📦 Prerequisites

Before you begin, make sure you have:

- A Google Cloud account
- `gcloud` CLI installed and authenticated
- `kubectl` installed
- Docker installed (if building and pushing images)

---

### 📁 Project Structure



├── manifests/
│   ├── db-deployment.yaml
│   ├── db-service.yaml
│   └── db-volume.yaml 
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   └── frontend-service.yaml
│
├── yolo-app-backend/           
├── yolo-app-frontend/          
└── README.md

### 🚀 Deploy the App

1. Create MongoDB with Persistent Volume

       kubectl apply -f db-volume.yaml 
       kubectl apply -f manifests/db-deployment.yaml
       kubectl apply -f manifests/mongo-service.yaml

2. Deploy the Yolo App Backend 

       kubectl apply -f manifestss/backend-deployment.yaml
       kubectl apply -f manifestss/backend-service.yaml

3. Deploy the Yolo App  Frontend

       kubectl apply -f k8s/frontend-deployment.yaml
       kubectl apply -f k8s/frontend-service.yaml

🌐 Accessing the App
  
  Once the frontend service is deployed, GKE will provision a LoadBalancer with an external IP.

📍 Access the frontend at:

   http://35.232.135.122
  
 
 
 # 🐳 YOLO App Provisioning with Ansible & Vagrant

This project provisions a local Ubuntu virtual machine using **Vagrant**, then uses **Ansible** to deploy the YOLO web application in Docker containers. The app stack includes:

- Frontend container
- Backend container
- MongoDB container with a persistent volume
- Docker network for inter-container communication

---

## 📦 Components

- **Ansible Roles:**
  
  - `docker` – Installs Docker Engine and Docker Compose plugin
  - `docker_network_and_volumes` – Sets up Docker network and MongoDB volume
  - `clone_repo` – Clones YOLO app source code from GitHub
  - `yolo_frontend` – Deploys frontend container
  - `yolo_backend` – Deploys backend container
  - `mongodb` – Deploys MongoDB container

## 🛠️ Prerequisites

- [Vagrant]
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- Internet connection (to pull Docker images and clone the Git repo)

---

##  Getting Started

### 1. Start the VM and run the provisioning

       vagrant up

 Vagrant will:

Spin up an Ubuntu virtual machine.

Run the Ansible provision.yml playbook automatically.

Deploy all containers using defined roles.

### 2. Access the app

- Frontend: http://localhost:3000

- Backend API: http://localhost:5000

-  MongoDB: Exposed on port 27017 

### 3. Running Specific Parts (with Tags)

You can target parts of the playbook using Ansible tags:

     vagrant provision --provision-with ansible -- --tags "frontend"

⚙️ Variables

Variables are centralized in group_vars/all.yml:

    frontend_image: kipten/yolo-app-frontend:v1.0.1
    backend_image: kipten/yolo-app-backend:v1.0.1
    mongodb_image: mongo:latest

    docker_network_name: yolo-net
    mongo_volume: mongo_db_data

    repo_url: https://github.com/kip1010ken/yolo
    repo_dest: /opt/yolo-app
    repo_branch: master

Update versions, ports, or the repo path as needed.


### 📁 Project Structure


    ├── README.md
    ├── Vagrantfile
    ├── ansible.cfg
    ├── inventory.yaml
    ├── provision.yaml
    ├── roles
    │   ├── clone_repo
    │   ├── docker
    │   ├── docker_network_and_volume
    │   ├── mongodb
    │   ├── yolo_backend
    │   └── yolo_frontend
