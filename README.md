# 📡 Jitsi Meet on Kubernetes with Custom Docker Images

### This project deploys a full Jitsi Meet video conferencing stack on Kubernetes using Docker images built, adapted for Kubernetes environments.

## 🧱 Components
### Prosody – XMPP server

### Jicofo – Conference focus component

### JVB – Jitsi Video Bridge (media router)

### Web – Nginx frontend with UI

## 📦 Prerequisites

### Kubernetes cluster (tested on K8s 1.28+)

### kubectl configured to talk to your cluster

### Docker (for building images, if not already pushed)

## 🛠️ AWS Setup: VPC, Subnets, Route Table, Internet Gateway and EC2 Instance

### 1. Create a VPC

   - **VPC Name:** `vpc-project`
   - **IPv4 CIDR block:** `10.0.0.0/24`
   - Set **Tenancy** as `Default`.


## 🛠️ EC2 Instance Setup

### 1. Launch EC2 Instance

   - **InstanceType:** t2.medium
   - **KeyName:** key.pair.pem
   - **VPC:** vpc-project
   - **SUBNET:** pub-sub-project
   - **SECURITY GROUP:** SSH (port 22) , HTTP (port 80) , HTTPS (port 443)

## 🚀 Deployment Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/riyaj-2002/jitsi-meet-app.git
cd jitsi-meet-app
```

### 2. Create Namespace
```bash
kubectl create namespace jitsi
```

### 3. Prepare Environment Variables
### Create a .env file based on your setup:

```bash
CONFIG=/home/ubuntu/.jitsi-meet-cfg
HTTP_PORT=8000
HTTPS_PORT=8443
TZ=Asia/Kolkata
PUBLIC_URL=https://<your-server-ip>:8443
JVB_ADVERTISE_IPS=<your-server-ip>
```

### 4. Create Kubernetes Secret
```bash
kubectl create secret generic jitsi-secret-env --from-env-file=.env -n jitsi
```

### 5. Deploy All Services
```bash
kubectl apply -f jitsi-prosody.yaml -n jitsi
kubectl apply -f jitsi-jicofo.yaml -n jitsi
kubectl apply -f jitsi-jvb.yaml -n jitsi
kubectl apply -f jitsi-web.yaml -n jitsi
```


## 🌐 Access the App
### Open in browser:
```bash
https://<external-ip>
```


     
