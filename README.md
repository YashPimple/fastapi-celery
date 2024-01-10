# FastAPI with Celery DevOps assessment

## Overview

This project demonstrates the deployment of a FastAPI application with Celery workers on Google Kubernetes Engine (GKE). The application uses Docker Compose for local development and a Kubernetes cluster for production deployment.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setup and Deployment](#setup-and-deployment)
3. [Scaling](#scaling)
4. [Approach](#approach)
5. [Pros & Cons](#pros)

## Prerequisites

Ensure you have the following tools installed:

- Docker
- Docker Compose
- Kubernetes cluster (GKE, EKS, AKS, etc.)

## Setup and Deployment

### Local Development
1. Run the following command to start the development environment:
```bash
docker-compose up
```
This command will start the FastAPI application, Celery workers, RabbitMQ, Redis, and Celery Flower for monitoring.
Further, open `http://localhost:8000` in your browser to interact with the FastAPI application.

## Approach: Learning Through Implementation

- I started up the assessment with the aim to learn more about Kubernetes and for that, I preferred GKE over managed Kubernetes services like Amazon EKS due to the fact that to learn and have more hands-on implementation of my skills within the Google cloud Ecosystem gaining more comprehensive understanding of GCP services.
- Firstly, started by setting up the project locally on my machine through the provided [readme]() file and it worked I was able to setup the whole project locally with the help of Docker and Docker-compose.
- Then moved on to developing a deployment Pipeline by Utilizing GitHub Actions to create a Continuous Deployment (CD) pipeline. Followed each and every step specify in the [docs](https://docs.google.com/document/d/1i1n-LFxODfKq0ro5VaTkHrIeMglCrHLP9tpVDZBAWB0/edit#heading=h.jdnogwyt9dvq).
  
- ### GitHub Actions:
  - Automated CD pipeline to be triggered whenever a pull request merges to the main branch.
  - Alongside writing script to build the docker image, pushing it to Artifact Registry, and deployment to GKE.
  - While Navigating through GitHub Actions the learning curve felt like deciphering a complex puzzle. Yet, the more I delved into its intricacies, the clearer the automation picture became. 

- ### Making use of Komposer to write K8 Manifests
    - [kompose](https://github.com/kubernetes/kompose) is a tool that takes a Docker Compose file and translates it into Kubernetes resources.
    - Installed and implemented it to generate Manifests from the `docker-compose.yaml` of our fast-api application
    - Additionally, Implemented Separate services for Redis and Celery within the Kubernetes further ensuring that these services are decoupled from the main application and can be       used by multiple applications concurrently.

## Pros:
1. Automated Scalability:
   - GKE's seamless integration with Kubernetes facilitates effortless scalability. The autoscaling capabilities ensure that our FastAPI application adapts dynamically to varying         workloads.
2. Managed Kubernetes Environment:
  - Leveraging GKE provides a managed Kubernetes environment, abstracting away infrastructure complexities. This allows me to focus more on the application logic rather than intricate cluster management.
3. Google Container Registry (GCR):
  - Integration with GCR simplifies Docker image storage and distribution. The central repository in GCP ensures efficient management and accessibility of container images.
4. Built-in Monitoring with Stackdriver:
  - GKE's powerful monitoring capabilities and native integration with Stackdriver bring forth powerful performance.

## Cons:
1. CI/CD Learning Curve:
  - Setting up an effective CI/CD pipeline for GKE came with its share of challenges. Configuring GitHub Actions to seamlessly build, push, and deploy Docker images required a deep dive into workflows and GKE authentication.
2. Kubernetes Complexity:
  - Navigating the intricacies of Kubernetes configurations demanded a learning curve. Understanding pod deployments, services, and persistent volumes presented challenges that   required thorough exploration and troubleshooting.
3. Autopilot Mode Constraints:
  - Initial attempts in GKE Autopilot mode faced constraints, particularly restrictions on host ports. Shifting to a standard GKE cluster was a workaround to overcome these challenges.


## Conclusion: Bridging the Knowledge Gap

In conclusion, the GKE deployment and CI/CD pipeline construction journey served as a bridge between theoretical knowledge and hands-on expertise. The process of grappling with challenges provided a deeper understanding of GCP tools and Kubernetes intricacies. The amalgamation of Docker, Kubernetes, GCR, and GitHub Actions has not only created a robust deployment pipeline but also enhanced my proficiency in orchestrating containerized applications on GKE.
