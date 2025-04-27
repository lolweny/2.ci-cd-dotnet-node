# 🚀 CI/CD Pipeline Project for .NET Application on Azure

## Overview

This project demonstrates building a full DevOps CI/CD pipeline to deploy a Dockerized .NET application to an Azure Virtual Machine (VM), using Terraform, Ansible, Docker, NGINX, and GitHub Actions.

I focused on automating infrastructure provisioning, application deployment, and securing the deployment with HTTPS.

---

## Project Structure

├── ansible/ # Ansible playbooks and inventory ├── app/ # .NET Core application ("Hello from .NET Web App") ├── terraform/ # Terraform IaC files for Azure resource provisioning ├── .github/workflows/ # GitHub Actions workflows (CI/CD pipeline) └── README.md # Project overview and documentation


---

## Tools & Technologies

- **Terraform**: Provision Azure Resource Group, Virtual Network, Subnet, Public IP, NSG, and Linux VM
- **Ansible**: Install NGINX, Docker, pull the Docker image from Azure Container Registry (ACR), and run the app container
- **Docker**: Containerize the .NET app
- **Azure Container Registry (ACR)**: Store the built Docker image
- **GitHub Actions**: Automate deployment using Ansible
- **NGINX**: Act as a reverse proxy and set up HTTPS with a self-signed SSL certificate
- **Azure VM**: Host the application

---

## How It Works

1. **Terraform** provisions:
   - Azure Resource Group
   - Virtual Network + Subnet
   - Public IP
   - Network Interface Card (NIC) + NSG
   - Ubuntu VM

2. **Dockerized .NET App** is built and pushed to ACR manually.

3. **Ansible Playbook**:
   - Installs NGINX and Docker
   - Logs into ACR
   - Pulls the Docker image
   - Runs the app container
   - Configures NGINX to proxy traffic with HTTPS (self-signed SSL)

4. **GitHub Actions**:
   - Automatically triggers Ansible playbook on workflow dispatch

---

## Challenges Faced

- **Azure Subscription Expired**: Midway through project, original free trial expired. I adapted by pushing everything cleanly to GitHub before moving on to a new subscription.
- **SSH & NSG Issues**: Had to manually recreate NSG rules (SSH, HTTP, HTTPS) to regain VM access.
- **Nginx Configuration Problems**: Dealt with missing directories (`/etc/nginx/sites-enabled`) and fixed them manually.
- **Terraform Image SKU Errors**: Adjusted Ubuntu image SKU names to match available Azure Marketplace images.
- **Permission Issues with Docker**: Resolved permission denied errors when using `docker ps` inside the VM.

These issues strengthened my ability to troubleshoot real-world Azure and DevOps problems.

---

## Lessons Learned

- Always monitor cloud subscription quotas during projects.
- Infrastructure-as-Code (IaC) improves reproducibility — resetting up the environment with Terraform saves a lot of time.
- Automation with Ansible ensures fast, repeatable deployments.
- Handling and recovering from errors (SSH lockouts, Docker issues, NGINX misconfigurations) is a key DevOps skill.

---

## How to Deploy (Simplified)

> If you want to recreate this project:

1. Clone this repository.
2. Update the Terraform files if needed (new Azure subscription IDs).
3. Run `terraform init` and `terraform apply` to provision infrastructure.
4. Push your Docker image to Azure Container Registry (ACR).
5. Set up SSH private key in GitHub secrets (`SSH_PRIVATE_KEY`) for Ansible.
6. Trigger the GitHub Actions workflow to run the Ansible deployment.
7. Visit the VM's public IP to see the app running behind HTTPS!

---

## Future Improvements

- Use Let's Encrypt certificates for free HTTPS instead of self-signed.
- Automate ACR Docker image build and push using GitHub Actions.
- Set up a domain name instead of accessing by public IP.

---

## Final Notes

Despite running into real-world cloud issues, I completed the project and built strong troubleshooting and automation experience.  
This project demonstrates my ability to deploy cloud infrastructure, containerized apps, automate deployments, and solve production-level problems.

---

