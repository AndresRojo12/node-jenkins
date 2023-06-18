pipeline {
    agent any

    stages {
        stage('Clonar el Repositorio') {
            steps {
                git branch: 'main', credentialsId: 'git-jenkins', url: 'https://github.com/AndresRojo12/node-jenkins.git'
            }
        }
        
        stage('Construir imagen de Docker') {
            steps {
                sh 'docker build -t proyecto-backend-microservicio:v1 .'
            }
        }
        
        stage('Desplegar contenedor Docker') {
            steps {
                sh 'docker run -d -p 80:80 --name proyecto-backend-microservicio proyecto-backend-microservicio:v1'
            }
        }
    }
}
