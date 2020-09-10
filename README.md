# GCP-Practice-Project
GADS 2020 Project submission

Labs:
1.Getting started with Cloud Marketplace
<img width="937" alt="Getting Started with Cloud Marketpalce" src="https://user-images.githubusercontent.com/54111426/92787497-73708d00-f3a9-11ea-93db-22a9bfff9415.png">
2. Getting started with Compute Engine
<img width="901" alt="Getting Started With Compute Engine" src="https://user-images.githubusercontent.com/54111426/92787911-cd715280-f3a9-11ea-977a-a9a15722149f.png">

3. Getting started with GKE
<img width="466" alt="Getting Started with GKE" src="https://user-images.githubusercontent.com/54111426/92788289-1a552900-f3aa-11ea-96c5-a2c98c5e18b2.png">

4. Getting started with App Engine
<img width="476" alt="Getting started with App Engine" src="https://user-images.githubusercontent.com/54111426/92788363-2ccf6280-f3aa-11ea-92a1-9f57e3b38fc8.png">

5. Getting Started with Deployment Manager and Cloud Monitoring
<img width="476" alt="Getting Started with Dep Manager and Cloud monitoring" src="https://user-images.githubusercontent.com/54111426/92788479-4375b980-f3aa-11ea-94f0-b1036f992541.png">

6. VPC Networking
<img width="479" alt="VPC Networking" src="https://user-images.githubusercontent.com/54111426/92788707-791aa280-f3aa-11ea-88e4-f5c8c9525d62.png">

7. Virtual Machines
<img width="481" alt="Virtual Machines" src="https://user-images.githubusercontent.com/54111426/92788843-92235380-f3aa-11ea-9145-cf2eed325910.png">

8. Implement Private Google Access and Cloud NAT
<img width="477" alt="Implement Private Google Access And Cloud NAT" src="https://user-images.githubusercontent.com/54111426/92788969-b3843f80-f3aa-11ea-8e77-f15f5c0fd0c8.png">

9. Creating Virtual Machines
<img width="479" alt="Creating Virtual Machines" src="https://user-images.githubusercontent.com/54111426/92789098-cc8cf080-f3aa-11ea-8cb3-7c0fdda91426.png">

10. Cloud IAM
<img width="467" alt="Cloud IAM" src="https://user-images.githubusercontent.com/54111426/92789187-e29ab100-f3aa-11ea-89ea-ea90ecd66390.png">

11. Cloud Storage
<img width="472" alt="Cloud Storage" src="https://user-images.githubusercontent.com/54111426/92789335-0a8a1480-f3ab-11ea-8ff8-a6d585707185.png">

12. Cloud SQL
<img width="473" alt="Cloud SQL" src="https://user-images.githubusercontent.com/54111426/92789420-1e357b00-f3ab-11ea-8096-fdf2b4026b95.png">

13. Configuring an Internal Load Balancer
<img width="472" alt="Configuring an Internal LB" src="https://user-images.githubusercontent.com/54111426/92789505-360cff00-f3ab-11ea-8b35-cb96ef920dc3.png">

14. Configuring an HTTP Load Balancer with Autoscaling
<img width="474" alt="Configuring an HTTP LB with Autoscaling" src="https://user-images.githubusercontent.com/54111426/92789604-4d4bec80-f3ab-11ea-86fb-5981551c69a9.png">

15. Virtual Private Networks
<img width="480" alt="Virtual Private Networks" src="https://user-images.githubusercontent.com/54111426/92789739-6a80bb00-f3ab-11ea-8257-f9afea93c171.png">



#Translation codes:
   1. Lab: Google Cloud Fundamentals: Getting started with compute engine.
   
 # Lab: Google Cloud Fundamentals: Getting started with compute engine.

#Objectives:
Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

Create a Compute Engine virtual machine using the gcloud command-line interface.

Connect between the two instances.

#Tasks:
1. Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default" --tags http

2. Create a Compute Engine virtual machine using the gcloud command-line interface.

gcloud config set compute/zone us-central1-b
gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

3.Connect between the two instances.

Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network.

Connect to my-vm-2 using ssh
   gcloud compute ssh my-vm-2
   run ping to test connection to my-vm-1
     ping my-vm-1

Use the ssh command to open a command prompt on my-vm-1
 ssh my-vm-1
  install the Nginx web server
    sudo apt-get install nginx-light -y

Use the nano text editor to add a custom message to the home page of the web server:
 sudo nano /var/www/html/index.nginx-debian.html

Add text like this, and replace YOUR_NAME with your name:
 Hi from YOUR_NAME

Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
 
 curl http://localhost/

To exit the command prompt on my-vm-1, execute this command.
 exit

To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:
 
 curl http://my-vm-1/

Get external IP for my-vm-1
 
 gcloud compute instances list

  copy and paste my-vm-1 external IP to a web browser address bar
you will see your web server's home page, including your custom text.

   2. Lab: Google Cloud Fundamentals: Getting Started with GKE
   
   #Google Cloud Fundamentals: Getting Started with GKE

#Objectives
Provision a Kubernetes cluster using Kubernetes Engine.

Deploy and manage Docker containers using kubectl.



#Tasks
1. Confirm that needed APIs are enabled Kubernetes Engine API and Container Registry API

     Enter following to display project ID
      gcloud projects list

    Set default project ID to one you want to enable APIs
      gcloud config set project YOUR_PROJECT_ID

    Get a list of services you can enable in your project
      gcloud services list --available

    If you dont see the API listed run following command
      gcloud services enable Kubernetes Engine API
      gcloud services enable Container Registry API

2. Start a Kubernetes Engine cluster

    set the zone your project is in to a variable called MY_ZONE
      export MY_ZONE=us-central1-a

    Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:
      gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

    After the cluster is created, check your installed version of Kubernetes using the kubectl version command
      kubectl version

    View your running nodes
      gcloud compute instances list

3. Run and deploy a container
    launch a single instance of the nginx container.
      kubectl create deploy nginx --image=nginx:1.17.10

    View the pod running the nginx container.
      kubectl get pods

    Expose the nginx container to the Internet
      kubectl expose deployment nginx --port 80 --type LoadBalancer

    View the new service
      kubectl get services

    Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed
    Scale up the number of pods running on your service
      kubectl scale deployment nginx --replicas 3

    Confirm that Kubernetes has updated the number of pods
      kubectl get pods

    Confirm that your external IP address has not changed
      kubectl get services
      
    Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.






