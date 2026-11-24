# Automated Portfolio Deployment on AWS Using Terraform and Ansible

## Project Overview

This project demonstrates automated infrastructure provisioning and configuration management using Terraform and Ansible.

Two Ubuntu EC2 instances are provisioned on AWS using Terraform. Ansible is then used to install and configure Apache2 on the first instance and Nginx on the second instance.

The same personal portfolio website is deployed to both web servers from the Ansible control node.

## Architecture

```text
                 Ansible Control Node
                   (Ubuntu Master)
                         |
                         | SSH
                         |
              +----------+----------+
              |                     |
        Ubuntu EC2 1           Ubuntu EC2 2
          (Apache2)               (Nginx)
              |                     |
          Port 80                 Port 80
              |                     |
       Portfolio Website     Portfolio Website
```

## Technologies Used

- AWS EC2
- Terraform
- Ansible
- Ubuntu Linux
- Apache2
- Nginx
- SSH
- Git and GitHub
- HTML, CSS and JavaScript

## AWS Infrastructure Provisioning Using Terraform

Terraform is used to provision two Ubuntu EC2 instances in the AWS Mumbai region (`ap-south-1`).

### Infrastructure Configuration

- Two Ubuntu EC2 instances
- Instance type: `t3.micro`
- AWS region: `ap-south-1`
- Public IPv4 address association
- Existing AWS EC2 Key Pair attached to both instances
- Security group allowing SSH, HTTP and HTTPS traffic

### Terraform Commands

Initialize Terraform:

```bash
terraform init
```

Validate configuration:

```bash
terraform validate
```

Review infrastructure changes:

```bash
terraform plan
```

Provision infrastructure:

```bash
terraform apply
```

Display EC2 public IP addresses:

```bash
terraform output
```

## Ansible Configuration Management

Ansible is installed on an Ubuntu machine, which acts as the control node.

The two EC2 instances are configured as managed nodes.

### Inventory Configuration

The inventory file defines two groups:

- `apache`: Ubuntu Server 1
- `nginx`: Ubuntu Server 2

SSH authentication is configured using an AWS EC2 private key.

### Test Connectivity

```bash
ansible all -m ping
```

### Apache2 Configuration

Ansible performs the following tasks on Ubuntu Server 1:

1. Updates the APT package cache.
2. Installs Apache2.
3. Starts the Apache2 service.
4. Enables Apache2 at system startup.
5. Deploys the portfolio website into `/var/www/html/`.

### Nginx Configuration

Ansible performs the following tasks on Ubuntu Server 2:

1. Updates the APT package cache.
2. Installs Nginx.
3. Starts the Nginx service.
4. Enables Nginx at system startup.
5. Deploys the portfolio website into `/var/www/html/`.

## Portfolio Deployment

The portfolio source code is stored on the Ansible control node.

Ansible's `copy` module transfers the website files to both EC2 instances.

Apache2 and Nginx serve the deployed portfolio website over HTTP.

### Execute Ansible Playbook

```bash
ansible-playbook webserver.yml
```

## Access the Deployed Website

After successful deployment, access the portfolio using the public IP addresses:

**Apache2 Server:**

```text
http://APACHE_PUBLIC_IP
```

**Nginx Server:**

```text
http://NGINX_PUBLIC_IP
```

Replace the placeholders with the actual EC2 public IP addresses.

## Verification

Check Apache2 status:

```bash
ansible apache -m command -a "systemctl is-active apache2"
```

Check Nginx status:

```bash
ansible nginx -m command -a "systemctl is-active nginx"
```

Verify the deployed websites:

```bash
curl http://APACHE_PUBLIC_IP
curl http://NGINX_PUBLIC_IP
```

## Project Directory Structure

```text
aws-portfolio-deployment/
│
├── terraform/
│   └── main.tf
│
├── ansible/
│   ├── ansible.cfg
│   ├── inventory.example
│   └── webserver.yml
│
├── portfolio/
│   ├── index.html
│   ├── CSS files
│   ├── JavaScript files
│   └── images/
│
├── .gitignore
└── README.md
```

## Key Learning Outcomes

- Infrastructure as Code using Terraform.
- Provisioning multiple AWS EC2 instances.
- Configuring SSH-based communication.
- Ansible inventory and playbook management.
- Automating Apache2 and Nginx installation.
- Deploying static websites using Ansible.
- Managing cloud infrastructure through automation.
- Version control using Git and GitHub.

## Future Enhancements

- Integrate Terraform and Ansible into a single automated workflow.
- Use dynamic inventory to retrieve EC2 instances automatically.
- Configure HTTPS using SSL certificates.
- Implement CI/CD using Jenkins.
- Use Ansible roles for reusable configurations.
- Deploy infrastructure across multiple Availability Zones.

## Author

**Sathishkumar**

Cloud Computing | AWS | Linux | Terraform | Ansible

GitHub: https://github.com/sathishkumar90437-blip

LinkedIn: www.linkedin.com/in/sathishkumar-n-h-075017293
