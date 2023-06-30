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
**kubectl apply -f mongo.yml**
**kubectl get deployment**
It will create Deployment, Replicaset and a POD.

Now, in the same file add Service component and apply it. It is a Internal service which is used for communication of PODS and other components.
**kubectl apply -f mongo.yml**
**kubectl get service**

It will create the Service the Deployment remains unchanged.


## Step 3:
Create mongo-configmap.yml file. This file holds URL of MongoDB so this file needs to be applied first because it reference will be used in mongo-express.yml file.
**kubectl apply -f mongo-configmap.yml**

## Step 4:
Now create mongo-express file. It is also combition of 2 components, Deployment and External Service. 
First apply only Deployment part 
**kubectl apply -f mongo-express.yml**
**kubectl get deployment*
**kubectl get pods**

This Deployment file contain Mongo-express image which will be the front end and this will talk with MongoDB using the credentials.

Now, the final step is to create the External Service in order to access MongoDB server through browser. 
This Service can be created in new file or we can use the same existing mongo-express file.

Add Secret part to the file and apply it
**kubectl apply -f mongo-express.yml**

It will create the Service the Deployment remains unchanged.

**kubectl get service**  will list the services. 
**minikube service mongo-express-service**
this command assign external Service a public IP address to the mongo-express server.

**minikube service mongo-express-server**
|-----------|----------------------|-------------|---------------------------|
| NAMESPACE |         NAME         | TARGET PORT |            URL            |
|-----------|----------------------|-------------|---------------------------|
| default   | mongo-express-server |        8081 | http://192.168.49.2:30001 |
|-----------|----------------------|-------------|---------------------------|
* Opening service default/mongo-express-server in default browser...
  http://192.168.49.2:30001

Open the IP in browser and access the MongoDB server.











