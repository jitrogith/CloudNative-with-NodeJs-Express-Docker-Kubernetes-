# CloudNative-with-NodeJs-Express-Docker-Kubernetes-

Let's Develop NodeJs with Docker & Kubernetes on AWS Amazon !

## 1. Install Ubuntu 18.04 server on EC2 Instance
Save your IP public for example http://55.55.55.55

## 2. Install NodeJs
    Browse https://www.cloudnativejs.io/
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
    
    Open browser and type http://55.55.55.55:3000

## 4. Create Dockerfile
    Open Docker path on https://www.cloudnativejs.io/
    
## 5. Upload Image to Dockerhub
## 6. Install Kubernetes
## 7. Download/ pull Image from Dockerhub
## 8. Helm
    Install Helm
    $ mkdir /opt/download
    $ snap install helm --classic
    $ helm repo add stable https://kubernetes-charts.storage.googleapis.com/
    
    Open Kubernetes path on https://www.cloudnativejs.io/
    Download MasterChart (Master.zip) for Helm
    $ cd /opt/download
    $ wget https://github.com/CloudNativeJS/helm/archive/master.zip
    $ unzip master.zip
    Install pod
    $ helm install nodeserver chart/nodeserver
    
    Delete & Upgrade Pod with Helm
    
    Install Probe : Liveness & Readiness
    $ npm install @cloudnative/health-connect
    $ vim /opt/myApp/app.js
        let health = require('@cloudnative/health-connect')
        let healthcheck = new health.HealthChecker()
        app.use('/live', health.LivenessEndpoint(healthcheck))
    $ npm install
    $ npm start
    Browse http://55.55.55.55:3000/live
    
    Let's add Ping Checker !
    $ vim /opt/myApp/app.js
        let pingcheck = new health.PingCheck('example.com')
        healthcheck.registerLivenessCheck(pingcheck)
    $ npm install
    $ npm start
    Browse http://55.55.55.55:3000/live
    
    Let's add liveness & readiness check !
    $ vim /opt/myApp/app.js
        app.use('/live', health.LivenessEndpoint(healthcheck))
    $ npm install
    $ npm start
    Browse http://55.55.55.55:3000/live
    Browse http://55.55.55.55:3000/ready
    
    Let's build Image !
    $ docker build -t nodeserver-run -f Dockerfile-run .
    $ docker tag nodeserver-run rootdock/nodeserver:1.1.0
    $ docker login
    $ docker push rootdock/nodeserver:1.1.0
    
    Enable Liveness & Readiness on Chart:
    $ vim /opt/myApp/charts/nodeserver/values.yml
    UN-MARKING/DELETE'#' to be like this (this PART Only) :
          ...
          tag: 1.1.0    # make sure it has same Image's version as created before !
          ...
          readinessProbe:
            httpGet:
              path: /ready
              port: 3000
            initialDelaySeconds: 3
            periodSeconds: 5
          livenessProbe:
            httpGet:
              path: /live
              port: 3000
            initialDelaySeconds: 40
            periodSeconds: 10
          ...
          
    $ helm upgrade nodeserver chart/nodeserver
    
## 9. Prometheus
    Download Prometheus from https://prometheus.io/download/
    Install
    $ tar xvfz prometheus-*.tar.gz
    $ cd prometheus-*
    $ vim prometheus.yml              >> edit if you want, for now we leave it as is
    $ ./prometheus -config.file=prometheus.yml
    Open Browser http://55.55.55.55:9090 and it will guide you to http://55.55.55.55:9090/graph
    
## 10. Grafana
