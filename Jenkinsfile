pipeline {
    agent any 

    stages {
        stage ("Build Docker Image"){
            steps {
                script {
		    dockerapp = docker.build("gabrieloliver01/kube-news:v1", '-f ./src/Dockerfile ./src')
				}
            }
        }

        stage ("Push Docker Image"){
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push('v1')
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
