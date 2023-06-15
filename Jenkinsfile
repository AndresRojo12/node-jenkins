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
                        docker.build('proyecto-backend-microservicio:v1', '--build-arg URI_MONGO=${URI_MONGO} .')
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
                        sh """
                            sed 's|\\${URI_MONGO}|${URI_MONGO}|g' docker-compose.yml > docker-compose-update.yml
                            docker-compose -f docker-compose-update.yml up -d
                        """
                    }
                }
            }
        }
    }
}
