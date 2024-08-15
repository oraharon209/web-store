# Web Store Application

Welcome to the **Web Store Application** repository! This project is a fully containerized web application that represents a store, providing users with the ability to browse, select, and manage products. A GitHub Action workflow has been implemented to ensure continuous integration and deployment of the application.

## Features

- **Frontend**: User-friendly interface built with Flask to navigate the store, view products, and manage shopping carts.
- **Backend**: Robust backend implemented with Flask, handling product data, user sessions, and order processing.
- **Database**: Integrated with MongoDB for efficient storage and retrieval of product and user data.
- **Event Streaming**: Utilizes Kafka for real-time event processing, ensuring smooth operations and data consistency.
- **Containerization**: Fully containerized using Docker, ensuring easy deployment and scalability.
- **Deployment**: Managed with Helm charts and Argo CD for automated deployment on Kubernetes clusters, specifically on AWS EKS.

## Architecture

The Web Store Application is composed of the following main components:

- **Frontend**: Flask-based UI for user interaction.
- **Backend**: Flask-based API to manage store operations.
- **Database**: MongoDB for storing product and user information, configured via Kubernetes manifest files.
- **Event Streaming**: Kafka for managing event-driven actions, also configured via Kubernetes manifest files.
- **Container Orchestration**: Deployed on AWS EKS, utilizing Helm charts for managing Kubernetes resources.
- **Continuous Deployment**: Integrated with Argo CD for automatic updates and deployments whenever there is a source code update.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Kubernetes cluster up and running.
- ArgoCD installed and configured on your Kubernetes cluster.
- Helm installed on your local machine.
- Docker installed for building images.

## Getting Started

To use this project properly, you should create separate GitHub repositories for the source code (`web-app-source`) and deployment configuration (`web-app-store`):

1. **Create GitHub Repositories**:
   - Create a repository named `web-app-source` to host the source code for both the backend and frontend.
   - Create a repository named `web-app-store` to host the Helm charts and Kubernetes manifests for deployment.

2. **Clone the repositories**:
   ```bash
   git clone https://github.com/yourusername/web-app-source.git
   git clone https://github.com/yourusername/web-app-store.git
   ```

3. **Create Docker Images**:
   - Navigate to the `web-app-source/backend` directory and build the Docker image:
     ```bash
     cd web-app-source/backend
     docker build -t your-backend-image-name .
     ```
   - Navigate to the `web-app-source/frontend` directory and build the Docker image:
     ```bash
     cd ../frontend
     docker build -t your-frontend-image-name .
     ```

4. **Modify the `values.yaml` File and GitHub Workflow**:
   - Navigate to the `web-app-store` directory.
   - Modify the `values.yaml` file according to your environment and configuration needs (e.g., database connection strings, Kafka configurations, Docker image names, etc.).
   - Additionally, modify the `.github/workflow` files(in both repos) to ensure the CI/CD pipeline is correctly configured to build and deploy the application based on your repository settings.

5. **Configure Argo CD**:
   - Ensure that Argo CD is set up in your Kubernetes cluster.
   - Link the `web-app-store` repository with Argo CD so that any source updates trigger the deployment pipeline.
   - The pipeline will build a new Docker image and deploy the updated application using Helm charts.

6. **Deploy to Kubernetes**:
   - Use Helm to deploy the application:
     ```bash
     helm install web-store ./web-app-store/chart
     ```

7. **Access the Application**:
   - The application will be available via the configured Ingress or LoadBalancer service as per your Kubernetes setup.

## Project Structure

- `frontend/`: Contains the Flask-based frontend code.
- `backend/`: Contains the Flask-based backend code.
- `web-app-store/`: Contains Helm charts and Kubernetes manifests for deploying the application on Kubernetes.
- `web-app-store/.github/workflows/`: Contains CD pipeline definitions for automating deployments.
- `web-app-source/.github/workflows/`: Contains CI pipeline definitions for automating image building.
