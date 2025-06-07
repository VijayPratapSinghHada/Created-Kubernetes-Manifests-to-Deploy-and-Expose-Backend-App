<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create Kubernetes Manifests

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks3)

**Author:** Vijay Pratap Singh Hada  
**Email:** vijaypratapsinghhada9@gmail.com

---

## Create Kubernetes Manifests

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks3_b01876555)

---

## Introducing Today's Project!

In this project, I will learn how to create Kubernetes manifest files because these files tell Kubernetes exactly how to deploy and manage my backend application. I'll create a Deployment file to handle putting the app onto the cluster and a Service file to make it accessible to users

### Tools and concepts

I used Amazon EKS, eksctl, and Docker to set up and prepare my application for deployment on Kubernetes. Key concepts include using manifests to define desired states and containerization.



### Project reflection

I did this project today to learn how to create Kubernetes manifests and deploy a containerized application on Amazon EKS.

This project took me approximately 45 minutes of hands-on work and about 40 minutes for documentation, totaling around 1 hour and 25 minutes.

---

## Project Set Up

### Kubernetes cluster

To set up today's project, I launched a Kubernetes cluster. Steps I took to do this included starting an EC2 server, installing a tool called eksctl to help manage Kubernetes on AWS, creating a special role that gives the EC2 server permission to work with other AWS services, and finally using eksctl to build the EKS cluster itself. This prepares the environment for deploying applications using Kubernetes.

### Backend code

I retrieved the backend that I plan to deploy by installing Git on my EC2 instance and then cloning the project from my team member’s GitHub repository. Backend is the part of the app that manages data and handles requests behind the scenes so everything works smoothly for users. After cloning, I checked that the folder with all the project files had appeared on my EC2 instance. 

### Container image

Once I cloned the backend code, I built a container image because Kubernetes needs this image, which acts like a blueprint, to deploy my application correctly and consistently. I used Docker to do this. First, I installed Docker on my EC2 instance and made sure my user had the right permissions to run Docker commands without needing `sudo` all the time. Then, in the directory with the backend code and the Dockerfile, I ran the `docker build` command. This command reads the instructions in the Dockerfile and creates the container image, ready to be used for deployment.

I also pushed the container image to a container registry, because storing it in a central place like Amazon ECR allows Kubernetes to easily access it for deployment. To push the image to ECR, I first created a new repository in ECR. Then, I used the commands provided by ECR to log in, tag my local container image with the repository's address, and finally upload the tagged image to my ECR repository.

---

## Manifest files

Kubernetes manifests are like instruction manuals for Kubernetes, telling it exactly how to run your application. Manifests are helpful because they define the desired state of your app, such as which container images to use, how many copies of your app should be running, and how to make it available.

A Kubernetes deployment manages how your application is run and updated within the cluster. It makes sure that the desired number of copies of your application are running and handles rolling out updates or rolling back if something goes wrong. The container image URL in my Deployment manifest tells Kubernetes where to find the specific blueprint for my application's containers, ensuring it pulls the correct version to deploy.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks3_b01876554)

---

## Service Manifest

A Kubernetes Service exposes your application and directs network traffic to the correct running instances of your app, which are called pods. You need a Service manifest to tell Kubernetes how to make your application accessible. It acts like a traffic manager, defining how external or internal traffic reaches your application's pods, ensuring your app can communicate with users or other services.

The Service manifest sets up the deployment of a Flask application, defining its configuration in the flask-service.yaml file. This file specifies a Kubernetes Service named nextwork-flask-backend, which uses a selector to target pods labeled app: nextwork-flask-backend. The Service is configured with a NodePort type, exposing port 8080 and directing traffic to targetPort 8080 on the selected pods via the TCP protocol.


![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks3_b01876555)

---

## Deployment Manifest

Annotating the Deployment manifest helped me understand the structure and purpose of each part of the file because adding comments forced me to think about what each line and section does. By breaking it down, I learned how the manifest tells Kubernetes how to deploy and manage my application, from specifying the API version and resource type to defining the number of replicas, selecting the right pods, and configuring the containers and ports within those pods. It gave me a clearer picture of how Kubernetes works from a high level down to the container level.



A notable line in the Deployment manifest is the number of replicas, which means how many identical copies of my application I want Kubernetes to keep running. Pods are relevant to this because they are the smallest deployable units in Kubernetes and hold the containers running my application. The Deployment uses the replica count to ensure that the specified number of Pods, each containing my application's container, are always active and available.

One part of the Deployment manifest I still want to know more about is how resource limits like CPU and memory are defined because understanding this is important for managing how much power my application uses and preventing it from using too many resources in the cluster. Knowing how to set these limits will help me optimize performance and costs.

![Image](http://learn.nextwork.org/blissful_yellow_calm_donkey/uploads/aws-compute-eks3_6aae73e71)

---

---
