# mongoDB-with-minikube

Procedure: 
# Step 1:
First create mongo-secret.yml file, then apply it by cmd 
**kubectl apply -f mongo-secret.yml**
**kubectl get service**
This file contains the Username and Password to interact with MongoDB database and these username and password are encrypted using base64 technique.
Exmaple: echo -n "username" | base64  => this will generate the encypted text and copy in the file.
