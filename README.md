# CloudNative-with-NodeJs-Express-Docker-Kubernetes-

Let's Develop NodeJs with Docker & Kubernetes on AWS Amazon !

## 1. Install Ubuntu 18.04 server on EC2 Instance
Save your IP public for example http://55.55.55.55

## 2. Install NodeJs
    $ sudo apt-get install curl
    $ curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
    $ sudo apt-get install nodejs
    $ node -v
    $ npm -v
    $ npm install -g express-generator

## 3. Create project on /opt/myApp
    $ cd /opt
    $ express myApp
    $ npm install
    $ npm start
#### Open browser and type http://55.55.55.55:3000

## 4. Create Dockerfile
## 5. Upload Image to Dockerhub
## 6. Install Kubernetes
## 7. Download/ pull Image from Dockerhub
## 8. Helm
    Install pod
    Delete & Upgrade Pod with Helm
    Install Probe : Liveness & Readiness

## 9. Prometheus
## 10. Grafana
