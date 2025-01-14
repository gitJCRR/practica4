pipeline {
    agent any
    tools {
        maven 'Maven version 3.8.5'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/gitJCRR/practica4.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
