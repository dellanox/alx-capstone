# Project ReadMe: Jenkins, Docker Setup, and Plugin Overview

## Overview
This document serves as a comprehensive guide detailing the steps and configurations performed in the context of Jenkins and Docker setup, troubleshooting, and plugin management.

## Key Accomplishments

### 1. **Jenkins Installation Troubleshooting**
- **Issue**: Jenkins service failed to start due to using Java 11, which is unsupported.
- **Resolution**:
  1. Installed supported Java versions (Java 17 or Java 21).
  2. Configured the system to use the correct Java version using the `update-alternatives` command.
  3. Restarted Jenkins successfully after updating the Java runtime.

### 2. **Jenkins Plugins Overview**
The following plugins were reviewed and their purposes explained:

| **Plugin**                        | **Purpose**                                                                 |
|------------------------------------|-----------------------------------------------------------------------------|
| **Folders**                        | Organize jobs into hierarchical folders.                                   |
| **OWASP Markup Formatter**         | Provides secure HTML formatting to prevent XSS vulnerabilities.            |
| **Build Timeout**                  | Automatically terminates builds exceeding a specified timeout.             |
| **Credentials Binding**            | Securely inject credentials into build environments.                       |
| **Timestamper**                    | Adds timestamps to build logs for easier debugging.                        |
| **Workspace Cleanup**              | Cleans up workspace directories before/after builds.                       |
| **Ant**                            | Integrates Apache Ant build scripts.                                       |
| **Gradle**                         | Supports Gradle-based build automation.                                    |
| **Pipeline**                       | Enables Groovy-based build pipelines (Jenkinsfile).                        |
| **GitHub Branch Source**           | Discovers and builds branches/pull requests from GitHub.                   |
| **Pipeline: GitHub Groovy Libraries** | Allows use of shared Groovy libraries from GitHub in pipelines.            |
| **Pipeline Graph View**            | Provides a visual representation of pipeline stages and their statuses.    |
| **Git**                            | Integrates Git for source code management.                                 |
| **SSH Build Agents**               | Connects Jenkins to build agents over SSH.                                 |
| **Matrix Authorization Strategy**  | Provides role-based, fine-grained access control.                          |
| **PAM Authentication**             | Uses PAM for authenticating users.                                         |
| **LDAP**                           | Integrates LDAP for centralized user authentication.                       |
| **Email Extension**                | Enables customizable email notifications for builds.                       |
| **Mailer**                         | Provides basic email notifications.                                        |
| **Dark Theme**                     | Adds a dark UI theme for Jenkins.                                          |

### 3. **Docker Installation on Ubuntu**
- **Issue**: Docker CE packages were not found in the default Ubuntu repositories.
- **Resolution**:
  1. Added Docker's official APT repository to the system.
  2. Installed Docker CE, Docker CLI, and containerd using:
     ```bash
     sudo apt install docker-ce docker-ce-cli containerd.io
     ```
  3. Verified the installation using:
     ```bash
     docker --version
     sudo docker run hello-world
     ```
  4. Optionally configured Docker to run without `sudo` by adding the user to the `docker` group.

### 4. **System Setup and Configuration**
- Configured the default Java runtime for Jenkins.
- Ensured all dependencies for Docker and Jenkins were installed.
- Optimized security and user roles for Jenkins using Matrix Authorization and PAM Authentication.

## How to Replicate

### Setting Up Jenkins with Supported Java
1. Install Java 17 or Java 21:
   ```bash
   sudo apt install openjdk-17-jdk
   sudo apt install openjdk-21-jdk
   ```
2. Configure the default Java runtime:
   ```bash
   sudo update-alternatives --config java
   ```
3. Restart Jenkins:
   ```bash
   sudo systemctl restart jenkins
   ```

### Installing Docker on Ubuntu
1. Add Docker's official GPG key and APT repository:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
2. Install Docker CE:
   ```bash
   sudo apt update
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```
3. Verify the installation:
   ```bash
   docker --version
   sudo docker run hello-world
   ```

## Additional Notes
- Always ensure your system is updated before installing new packages.
- For Jenkins security, regularly update plugins and review user permissions.
- If Docker or Jenkins fails to start, refer to logs for troubleshooting:
  ```bash
  sudo journalctl -u docker
  sudo journalctl -u jenkins
  ```


