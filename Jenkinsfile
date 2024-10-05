pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone'){
            steps {git url:'https://github.com/UST-Training-B5/employee-service.git', branch:'main'}
        }
        stage('Build'){
            steps {bat "mvn clean install -DskipTests"}
        }
        stage('Test'){
            steps{bat "mvn test"}
        }
        stage('Deploy'){
            steps{
                bat "docker rm -f emp-container"
                bat "docker rmi -f emp-image"
                bat "docker build -t emp-image ."
                bat "docker run -p 8082:8082 -d --name emp-container emp-image"}
        }
    }
}