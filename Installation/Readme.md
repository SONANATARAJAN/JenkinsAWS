# Jenkins Installation and Overview Guide

This guide provides an overview of Jenkins, its features, and step-by-step instructions to install Jenkins on a Debian-based system. The content is designed to help users understand Jenkins and set it up effectively.

## What is Jenkins?

Jenkins is an open-source automation server written in Java. It facilitates continuous integration and continuous deployment (CI/CD) by automating the building, testing, and deployment of software projects. Jenkins is highly extensible, with a vast ecosystem of plugins that allow it to integrate with various tools and services, making it a popular choice for DevOps teams.

### Key Features
- **Continuous Integration/Continuous Deployment (CI/CD)**: Automates the process of integrating code changes, running tests, and deploying applications.
- **Extensive Plugin Ecosystem**: Over 1,800 plugins to integrate with tools like Git, Docker, Kubernetes, AWS, and more.
- **Pipeline Support**: Define build processes as code using Jenkins Pipeline, enabling complex workflows.
- **Distributed Builds**: Supports master-agent architecture to distribute workloads across multiple machines.
- **Customizable**: Highly configurable to suit various project needs, from simple builds to complex deployment pipelines.
- **Community Support**: Backed by a large community, providing extensive documentation and resources.

## Pre-Requisites

To install Jenkins on a Debian-based system (e.g., Ubuntu), ensure the following requirements are met:
- **Operating System**: Debian-based Linux distribution (e.g., Ubuntu 20.04 or later).
- **Java (JDK)**: Jenkins requires Java to run. OpenJDK 17 is recommended.
- **Hardware**: At least 1 GB of RAM and sufficient disk space for builds and artifacts.
- **Network**: Internet access for downloading Jenkins and plugins; port 8080 open for accessing the Jenkins web interface.
- **User Permissions**: Administrative (sudo) access to install packages.

## Installation Steps

Follow these steps to install Jenkins on a Debian-based system.

### 1. Install Java 
**System Update (Always First)**
```bash
sudo apt update
sudo apt upgrade -y
```

**Required Packages (Latest)**

```bash
  sudo apt install -y \
  openjdk-17-jdk \
  ca-certificates \
  curl \
  gnupg \
  lsb-release
```

🔹 Jenkins officially supports Java 17 (latest recommended)

Verify:
```bash
java -version
```

Jenkins Signing Key (Latest – Valid till 2028)
```bash
sudo mkdir -p /etc/apt/keyrings
gpg --keyserver keyserver.ubuntu.com --recv-keys 7198F4B714ABFC68
gpg --export 7198F4B714ABFC68 | sudo tee /etc/apt/keyrings/jenkins.gpg > /dev/null
```

Verify:
```bash
gpg --show-keys /etc/apt/keyrings/jenkins.gpg
```

**Jenkins Repository (Stable / LTS)**
echo "deb [signed-by=/etc/apt/keyrings/jenkins.gpg] https://pkg.jenkins.io/debian-stable binary/" \
| sudo tee /etc/apt/sources.list.d/jenkins.list

** Update Package Index**
```bash
sudo apt update
```

**Install Latest Jenkins (LTS)**
```bash
sudo apt install -y jenkins
```


**Check version:**
```bash
jenkins --version
```

** Start & Enable Jenkins Service**
```bash
sudo systemctl daemon-reexec
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```


### 3. Start and Enable Jenkins

Once installed, Jenkins runs as a systemd service. Start and enable the Jenkins service to ensure it runs automatically on system boot:

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Verify that Jenkins is running:

```bash
sudo systemctl status jenkins
```

The output should indicate that the Jenkins service is `active (running)`.

## Post-Installation Steps

1. **Access Jenkins**:
   - Open a web browser and navigate to `http://localhost:8080` (or `http://<server-ip>:8080` if accessing remotely).
   - Jenkins runs on port 8080 by default. Ensure this port is open in your firewall settings if necessary:
     ```bash
     sudo ufw allow 8080
     ```

2. **Unlock Jenkins**:
   - On first access, Jenkins will prompt you to unlock it using an initial admin password.
   - Retrieve the password from the server:
     ```bash
     sudo cat /var/lib/jenkins/secrets/initialAdminPassword
     ```
   - Copy the password and paste it into the Jenkins web interface to proceed.

3. **Complete Setup**:
   - Follow the on-screen instructions to complete the setup.
   - Choose **Install suggested plugins** for a standard setup, or select specific plugins based on your needs.
   - Create an admin user account and configure the Jenkins URL.

4. **Configure Jenkins**:
   - After setup, access the Jenkins dashboard to create jobs, configure pipelines, or install additional plugins via **Manage Jenkins > Manage Plugins**.

## Basic Usage

- **Create a Job**:
  - From the Jenkins dashboard, click **New Item**, choose a job type (e.g., Freestyle project or Pipeline), and configure the job settings.
  - Link to a version control system (e.g., Git) and define build steps (e.g., shell commands, tests, or deployments).

- **Set Up Pipelines**:
  - Use Jenkins Pipeline to define build processes as code. Create a `Jenkinsfile` in your repository to describe the pipeline stages.

- **Monitor Builds**:
  - View build history, logs, and statuses from the Jenkins dashboard to monitor job execution.

## Troubleshooting

- **Jenkins Not Starting**:
  - Check the Java version (`java -version`) to ensure compatibility.
  - Review Jenkins logs: `sudo journalctl -u jenkins`.

- **Port Conflicts**:
  - If port 8080 is in use, modify the Jenkins configuration file (`/etc/default/jenkins`) to change the `HTTP_PORT`.

- **Plugin Installation Issues**:
  - Ensure internet connectivity and check the plugin manager for errors.

## Additional Notes

- **Upgrading Jenkins**:
  - Regularly update Jenkins using:
    ```bash
    sudo apt-get update
    sudo apt-get install jenkins
    ```

- **Backup**:
  - Back up the `~/.jenkins` directory (or `/var/lib/jenkins` for system-wide installations) to preserve configuration and job data.

- **Security**:
  - Configure authentication and authorization in **Manage Jenkins > Configure Global Security**.
  - Use SSL for secure access by configuring a reverse proxy (e.g., Nginx or Apache).

For more information, refer to the official [Jenkins Documentation](https://www.jenkins.io/doc/).
