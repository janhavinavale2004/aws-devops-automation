# AWS DevOps Automation Project

## Project Overview

This project demonstrates a complete CI/CD pipeline for deploying a Flask application using AWS, Jenkins, Docker, Docker Hub and Kubernetes.

## Architecture

Developer
↓
GitHub Repository
↓
GitHub Webhook
↓
Jenkins CI/CD Pipeline
↓
Run Python Tests
↓
Build Docker Image
↓
Push Image to Docker Hub
↓
Deploy to Kubernetes
↓
Flask Application

## Technologies Used

- AWS EC2
- Terraform
- Git and GitHub
- Jenkins
- Python Flask
- Docker
- Docker Hub
- Kubernetes (K3s)
- Linux

## CI/CD Pipeline Stages

1. Checkout Code
2. Run Python Tests
3. Build Docker Image
4. Push Image to Docker Hub
5. Deploy to Kubernetes
6. Verify Deployment

## How It Works

When a developer pushes code to GitHub, a GitHub webhook automatically triggers the Jenkins pipeline.

Jenkins runs automated tests, builds a Docker image and pushes it to Docker Hub.

Jenkins then deploys the updated Docker image to Kubernetes.

## Project Features

- Automated testing
- Automated Docker image creation
- Docker Hub integration
- Kubernetes deployment
- Jenkins CI/CD automation
- GitHub webhook trigger
- Infrastructure provisioning using Terraform

## Author

Janhavi Navale
