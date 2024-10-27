# AWS CD pipeline example

#### Description
This project serves as an example project on how to setup
a CI/CD pipeline github actions and AWS as the cloud provider.

## Setup
### Pre-requisites
- asdf (https://asdf-vm.com/)  
  - asdf Gradle plugin (https://github.com/rfrancis/asdf-gradle)  
  - Java plugin (https://github.com/halcyon/asdf-java)

### Install dependencies
```bash
asdf install
```

### Run locally
```bash
./gradlew bootRun
```
Test by opening a browser to http://localhost:8080/actuator/health


### Manually Deploy to EC2 server

#### Create an EC2 instance
- Log in to [the AWS Management Console](https://aws.amazon.com/console/)
- Navigate to the EC2 Dashboard and click on Launch Instance
- Select an Amazon Machine Image (AMI): Choose a Amazon Linux
- Choose an Instance Type: e.g., t2.micro (eligible for the free tier).
- Configure Security Group: 
  - Inbound: SSH (22) and App (8080) from anywhere
  - Outbound: HTTP and HTTPS from anywhere
- Review and launch the instance. Download the key pair to access your server as PEM.
- Connect to the instance using SSH

#### Setup the server
```bash
ssh -i /path/to/your-key.pem ec2-user@ec2-public-dns-name
sudo yum install java-21-amazon-corretto-headless -y
java -version
```

#### Deploy the application
```bash
./gradlew build -x test
scp -i ~/Downloads/your-key.pem build/libs/aws-cd-example-0.0.1-SNAPSHOT.jar ec2-user@ec2-public-dns-name:/home/ec2-user/               ─╯
```

#### Run the app
```bash
java -jar aws-cd-example-0.0.1-SNAPSHOT.jar
```
Test accessing http://ec2-public-dns-name:8080/actuator/health

### Auto deploy on Github action

#### Prepare repository secrets
1. In your GitHub repository, go to Settings > Secrets and variables > Actions.
2. Add the following secrets:
  - EC2_HOST: The public IP address or hostname of your EC2 instance.
  - EC2_USER: The SSH user for your EC2 instance (e.g., ec2-user for Amazon Linux, ubuntu for Ubuntu).
  - EC2_KEY: Your EC2 instance’s private key. Copy the private key file’s contents and paste it here.

#### Deploy with new changes From [ec2-deploy.yml](.github/workflows/ec2-deploy.yml)
- Push your changes to the `aws_ec2_ssh` branch.  
Test accessing http://ec2-public-dns-name:8080/actuator/health