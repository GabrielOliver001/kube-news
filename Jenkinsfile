pipeline {
    agent any 

    stages {
        stage ("Build Docker Image"){
            steps {
                script {
                    docker app = docker.build("gabrieloliver001/kube-news:v1", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage ("Push Docker Image"){
            steps {
                sh "echo 'Envio da Imagem'"
            }
        }

        stage ("Deploy no Kubernetes"){
            steps {
                sh "echo 'Deploy no Kubernetes'"
            }
        }
    }
}
