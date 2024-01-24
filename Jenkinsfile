pipeline {
    agent any 

    stages {
        stage("Get Source"){
            steps {
                git url: 'https://github.com/GabrielOliver001/kube-news.git', branch: 'main'
            }
        }
        stage("Build Docker Image"){
            steps {
                script{
                    docker.build("gabrieloliver001-kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
                
        }

        stage("Push Docker Image"){
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }

        stage("Deploy no Kubernetes"){
            steps {
                sh "echo 'Deploy no Kubernetes'"
            }
        }
    }
}
