# mongoDB-with-minikube

Procedure: 
## Step 1:
First create mongo-secret.yml file, then apply it by cmd 
**kubectl apply -f mongo-secret.yml**
**kubectl get service**
This file contains the Username and Password to interact with MongoDB database and these username and password are encrypted using base64 technique.
Exmaple: **echo -n "username" | base64**  => this will generate the encypted text and copy in the file.
This Secret has the reference inside MongoDB Deployment file.

## Step 2:
Create mongo.yml file. The file contain two components, first is Deployment and second is Service
First take only deployment code then apply it
**kubectl apply -f mongo.yml
kubectl get deployment
**
It will create Deployment, Replicaset and a POD.
Now, in the same file add Service component and apply it. It is a Internal service which is used for communication of PODS and other components.
kubectl apply -f mongo.yml
kubectl get service
