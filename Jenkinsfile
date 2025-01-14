pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/gitJCRR/practica4.git'
            }
        }
        stage('Build') {
            steps {
                 powershell 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                 powershell 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                     powershell 'mvn sonar:sonar'
                }
            }
        }
    }
}
