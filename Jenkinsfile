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
                script {
                    withCredentials([
                        string(credentialsId: 'URI_MONGO', variable: 'URI_MONGO')
                    ]) {
                        sh 'docker build -t proyecto-backend-microservicio:v1 --build-arg URI_MONGO=${URI_MONGO} .'
                    }
                }
            }
        }
        stage('Desplegar contenedores Docker') {
            steps {
                script {
                    withCredentials([
                        string(credentialsId: 'URI_MONGO', variable: 'URI_MONGO')
                    ]) {
                        sh '''
                            docker-compose up -d
                        '''
                    }
                }
            }
        }
    }
}
