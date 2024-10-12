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