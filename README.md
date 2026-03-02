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

### 3. Create Kubernetes Secret
```bash
kubectl create secret generic jitsi-secret-env -n jitsi \
  --from-literal=PUBLIC_URL=http://<YOUR_PUBLIC_IP> \
  --from-literal=HTTP_PORT=80 \
  --from-literal=HTTPS_PORT=443 \
  --from-literal=TZ=UTC \
  --from-literal=XMPP_DOMAIN=jitsi-prosody \
  --from-literal=XMPP_AUTH_DOMAIN=auth.jitsi-prosody \
  --from-literal=XMPP_INTERNAL_MUC_DOMAIN=internal-muc.jitsi-prosody \
  --from-literal=XMPP_MUC_DOMAIN=muc.jitsi-prosody \
  --from-literal=XMPP_SERVER=jitsi-prosody \
  --from-literal=JICOFO_AUTH_USER=focus \
  --from-literal=JICOFO_AUTH_PASSWORD=focuspassword \
  --from-literal=JVB_AUTH_USER=jvb \
  --from-literal=JVB_AUTH_PASSWORD=jvbpassword \
  --from-literal=JVB_BREWERY_MUC=jvbbrewery \
  --from-literal=JVB_ADVERTISE_IPS=<YOUR_PUBLIC_IP> \
  --from-literal=DOCKER_HOST_ADDRESS=<YOUR_PUBLIC_IP>
```

### 4. Deploy All Services
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

## Updating
### If you want to update, simply run (Finds the latest release of docker-jitsi-meet on GitHub)
```bash
wget $(curl -s https://api.github.com/repos/jitsi/docker-jitsi-meet/releases/latest | grep 'zip' | cut -d\" -f4)
```

     
