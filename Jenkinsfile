pipeline {
    agent any

    stages {
        stage('Build Eureka Service') {
            steps {
               checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Jagmeet-Singh-Tiwana/Eureka-svc.git']])
               bat 'mvn clean install'
            }
        }
         stage('Build Eureka Service Docker Image') {
            steps {
              bat 'docker build -t jagmeet/eureka-svc .'
            }
        }
         stage('Run Eureka Service') {
            steps {
              bat 'docker rm eureka-cont'
              bat 'docker run -d --name eureka-cont --network stud-network -p 8761:8761 jagmeet/eureka-svc'
            }
        }
        stage('Run Eureka Service') {
            steps {
                 build 'student-job'
            }
        }
       
    }
}
