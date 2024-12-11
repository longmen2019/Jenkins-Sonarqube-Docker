

```markdown


# Jenkins-Sonarqube-Docker Project

This project demonstrates how to set up Jenkins, SonarQube, and Docker on an AWS EC2 instance to create a CI/CD pipeline for code quality analysis and continuous integration.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- Docker
- Docker Compose
- Jenkins
- SonarQube

## Setup Instructions

### Step 1: Launch an EC2 Instance

1. **Log in to AWS Management Console** and navigate to the EC2 Dashboard.
2. **Launch a new instance**:
   - Choose the **Ubuntu Server 20.04 LTS** Amazon Machine Image (AMI).
   - Select the **t2.medium** instance type.
   - Configure the instance details and add storage as needed.
   - **Create a new key pair** or use an existing one.
   - **Configure the security group** to allow SSH (port 22), HTTP (port 80), and custom TCP rules for Jenkins (port 8080) and SonarQube (port 9000).
   - Review and launch the instance.

### Step 2: Connect to Your EC2 Instance

1. **Open your terminal** and connect to the instance using SSH.
   ```sh
   ssh -i /path/to/your-key-pair.pem ubuntu@your-ec2-public-ip
   ```
   Replace `/path/to/your-key-pair.pem` with the path to your key pair file and `your-ec2-public-ip` with your instance's public IP address.

### Step 3: Install Docker

1. **Update the package index** and install Docker.
   ```sh
   sudo apt-get update
   sudo apt-get install docker.io -y
   ```
2. **Start and enable Docker**.
   ```sh
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

### Step 4: Install SonarQube

1. **Create a new user** for SonarQube.
   ```sh
   sudo adduser --system --no-create-home --group --disabled-login sonarqube
   ```
2. **Download and install SonarQube**.
   ```sh
   cd /tmp
   sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip
   sudo unzip sonarqube-9.9.0.65466.zip -d /opt
   sudo mv /opt/sonarqube-9.9.0.65466 /opt/sonarqube
   sudo chown -R sonarqube:sonarqube /opt/sonarqube
   ```

### Step 5: Install Jenkins

1. **Add the Jenkins repository key** and source list.
   ```sh
   wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
   sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
   ```
2. **Update the package index** and install Jenkins.
   ```sh
   sudo apt-get update
   sudo apt-get install jenkins -y
   ```
3. **Start and enable Jenkins**.
   ```sh
   sudo systemctl start jenkins
   sudo systemctl enable jenkins
   ```
4. **Configure the firewall** to allow traffic on port 8080.
   ```sh
   sudo ufw allow 8080
   sudo ufw enable
   ```

### Step 6: Access Jenkins and SonarQube

1. **Access Jenkins** at `http://your-ec2-public-ip:8080`.
2. **Access SonarQube** at `http://your-ec2-public-ip:9000`.

### Step 7: Configure Jenkins

1. **Install the necessary plugins**:
   - Docker Pipeline
   - SonarQube Scanner
2. **Configure Jenkins to use the SonarQube server**:
   - Go to **Manage Jenkins** > **Configure System**.
   - Add a new SonarQube server with the following details:
     - **Name**: SonarQube
     - **Server URL**: `http://localhost:9000`
     - **Authentication Token**: (Generate a token from SonarQube and add it here)

## Project Structure

```plaintext
Jenkins-Sonarqube-Docker/
├── Dockerfile
├── Jenkinsfile
├── index.html
├── prepros.config
├── test.txt
├── vendor/
└── README.md
```

## Contributing

If you would like to contribute to this project, please fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

Special thanks to the creators of Jenkins, SonarQube, and Docker for their amazing tools.

## Resources

- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [SonarQube Documentation](https://docs.sonarqube.org/)
- [Docker Documentation](https://docs.docker.com/)

## Reference

- [YouTube Video: Jenkins, SonarQube, and Docker Setup](https://www.youtube.com/watch?v=361bfIvXMBI&t=2705s)
```
