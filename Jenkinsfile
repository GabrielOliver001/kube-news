pipeline {
    agent any 

    stages {
        stage ("Build Docker Image"){
            steps {
                script {
		    dockerapp = docker.build("gabrieloliver001/kube-news:latest", '-f ./src/Dockerfile ./src')
		}
            }
        }

        stage ("Push Docker Image"){
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub'){
                        dockerapp.push('latest')
                        
                    }
                }
            }
        }

        stage ("Deploy no Kubernetes"){
            steps {
                sh "echo 'Deploy no Kubernetes'"
            }
        }
    }
}
