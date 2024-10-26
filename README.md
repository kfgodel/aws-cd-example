# Heroku CLI CD pipeline example

#### Description
This project serves as an example project on how to setup
a CI/CD pipeline using Heroku CLI.

## Setup
### Pre-requisites
- asdf (https://asdf-vm.com/)  
  - asdf Gradle plugin (https://github.com/rfrancis/asdf-gradle)  
  - Java plugin (https://github.com/halcyon/asdf-java)
- Brew (https://brew.sh/)
- Heroku CLI (https://devcenter.heroku.com/articles/heroku-cli)

### Install dependencies
```bash
asdf install
brew tap heroku/brew && brew install heroku
heroku --version
```

### Run locally
```bash
./gradlew bootRun
```
Test by opening a browser to http://localhost:8080/actuator/health

### Deploy to Heroku
```bash 
heroku login
heroku create
git push heroku heroku_cli_cd:main
```
Test by opening a browser to https://enigmatic-retreat-23023-8d15c8c2b578.herokuapp.com/actuator/health

