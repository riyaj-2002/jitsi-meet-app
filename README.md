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


     
