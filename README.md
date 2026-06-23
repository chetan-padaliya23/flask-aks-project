flask-aks-project
Overview
End-to-end CI/CD project — Flask app ko GitHub Actions ke through automatically Docker Hub pe push karna aur Azure Kubernetes Service (AKS) pe deploy karna. Load Balancer ke through publicly accessible hai taaki high traffic pe multiple pods kaam kar sakein.
Architecture
GitHub Push (main branch)
        ↓
GitHub Actions Pipeline
        ↓
Docker Build + Push → Docker Hub
        ↓
Azure Login (OIDC)
        ↓
AKS Set Context
        ↓
kubectl apply → AKS Cluster
        ↓
LoadBalancer Service → Public IP
Technologies Used
TechnologyPurposePython + FlaskWeb applicationDockerContainerizationDocker HubContainer registryGitHub ActionsCI/CD pipelineAzure Kubernetes ServiceContainer orchestrationOIDCPasswordless Azure authenticationGit Bash / Azure PowerShellLocal setup & cluster management
Pipeline Flow
Build Job:

Checkout code
Login to Docker Hub
Build Docker image
Push to Docker Hub (chetan2308/flask-aks-app:latest)

Deploy Job: (runs after build)

Checkout code
Azure login via OIDC
Set AKS context
kubectl apply — Deployment + Service

Prerequisites

AKS cluster already created
GitHub Secrets set karne padenge:

DOCKER_USERNAME
DOCKER_PASSWORD
AZURE_CLIENT_ID
AZURE_TENANT_ID
AZURE_SUBSCRIPTION_ID


OIDC Federated Credential configured in Azure App Registration

Problems Faced & Fixed
ProblemFixImagePullBackOffDocker Hub image name galat tha, sahi naam diyaPipeline push failPAT mein workflow scope missing thaDockerfile not foundcontext: ./app karna pada instead of .
What I Learned

Kubernetes Deployment aur LoadBalancer Service kaise likhte hain
GitHub Actions se AKS pe automated deployment
OIDC se passwordless Azure authentication
Docker image build aur push pipeline mein integrate karna
kubectl se cluster debug karna# flask-aks-project