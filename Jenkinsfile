pipeline {
    agent any
    tools {
        maven 'Maven 3.9.9'
        jdk 'JDK 17' // Cambiar según el JDK configurado en Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/gitJCRR/practica4.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Comando Maven para limpiar e instalar dependencias, forzando la actualización
                    bat 'mvn clean install -U'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Ejecutar pruebas y generar informes
                    bat 'mvn test'
                }
            }
            post {
                always {
                    // Publicar los resultados de JUnit
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube Analysis') {
                    powershell 'mvn sonar:sonar'
                }
            }
        }
    }
    post {
        failure {
            // Notificación de errores
            echo 'Pipeline falló. Revisa las etapas anteriores.'
        }
        success {
            echo 'Pipeline completado exitosamente.'
        }
    }
}
