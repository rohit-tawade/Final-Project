# 🎬 Online Movie Ticket Booking App - Full Deployment Automation

This project automates the deployment of a **Flask-based Movie Ticket Booking Web App** using **Terraform**, **Ansible**, **Docker**, and **GitHub Actions** on an **AWS EC2** instance.  
It includes provisioning the EC2 instance, configuring Docker, and deploying the app with CI/CD.

---

## 📁 Project Structure

```
.
├── .github/
│   └── workflows/
│       ├── ansible-deploy.yml         # GitHub Actions to run Ansible playbook
│       └── terraform-deploy.yml       # GitHub Actions to provision EC2 via Terraform
│
├── Ansible/
│   ├── deploy.yml                     # Main Ansible playbook
│   └── inventory.ini                  # Hosts (EC2 public IP)
│
├── OnlineMovieTicketBooking-Python/   # Flask project directory
│   ├── DATABASE FILE/                 # SQL DB schema
│   ├── static/                        # CSS, JS, images
│   ├── templates/                     # HTML templates
│   ├── app.py                         # Flask main app
│   ├── Dockerfile                     # Dockerfile for app container
│   ├── .dockerignore
│   ├── 01 LOGIN DETAILS.txt           # Credentials/Info (exclude in production!)
│   └── README.md
│
├── Terraform/
│   ├── main.tf                        # Terraform EC2 provisioning script
│   └── README.md                      # Terraform-specific instructions
│
└── README.md
```

---

## 🔧 Prerequisites

- AWS Account (with IAM user & access keys)
- SSH Key pair (`.pem` file) for EC2 login
- GitHub account with this repo
- DockerHub account to store image
- Custom domain (e.g., purchased via Route 53 or another registrar)

---

## 🚀 Step-by-Step Deployment

### 1. 🖥️ Build & Push Docker Image

```bash
cd OnlineMovieTicketBooking-Python/
docker build -t rohitdocker143/movie-booking-app:latest .
docker push rohitdocker143/movie-booking-app:latest
```

---

### 2. ☁️ Provision EC2 using Terraform

```bash
cd Terraform/
terraform init
terraform apply
```

✅ Note the EC2 public IP from the output.

---

### 3. 🔐 Configure SSH Access for Ansible

Update `Ansible/inventory.ini`:

```ini
[web]
<EC2_PUBLIC_IP> ansible_user=ec2-user
```

Store the private key in GitHub:

- Go to **Repo → Settings → Secrets and Variables → Actions**
- Add secret:
  - **Name:** `EC2_SSH_KEY`
  - **Value:** Paste your `.pem` file contents

---

### 4. 🤖 GitHub Actions CI/CD

Push to `main` branch triggers:

1. `terraform-deploy.yml` → Provisions EC2  
2. `ansible-deploy.yml` → Installs Docker, pulls image, runs app

Or run manually:

```bash
cd Ansible/
ansible-playbook -i inventory.ini deploy.yml --private-key ~/.ssh/Linux-Key.pem
```

---

## 🌐 Access the App

```bash
http://<EC2_PUBLIC_IP>/
```

You should see the Movie Booking web app live!

---

## 🌍 Custom Domain with Route 53

Map your app to a domain using **Amazon Route 53**.

### ✅ Steps:

1. **Buy/Register a domain**  
   - Go to [Route 53 Console](https://console.aws.amazon.com/route53/)  
   - Register or transfer a domain

2. **Create a Hosted Zone**  
   - Click **Hosted Zones → Create Hosted Zone**  
   - Enter your domain (e.g., `rohit-portfolio.me`)

3. **Create an A Record**  
   - In Hosted Zone → **Create Record**  
   - Record Type: `A – IPv4 address`  
   - Value: Your EC2 Public IP  
   - TTL: Default (300 seconds)  
   - Click **Create records**

4. **Wait for DNS Propagation**  
   - Visit: `http://rohit-portfolio.me`  
   - You should see your deployed app

---

## 🧹 Clean Up

```bash
cd Terraform/
terraform destroy
```

---

## ✍️ Author

**Rohit Santram Tawade**  
[GitHub](https://github.com/rohit-tawade) • [DockerHub](https://hub.docker.com/u/rohitdocker143)

---

## 📜 License

This project is open-source and licensed under the **MIT License**.
