pipeline {
    agent any 
    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub'
    }
    stages {
        stage ("Build Docker Image"){
            steps {
                script {
		    withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')])
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
		    dockerapp = docker.build("gabrieloliver001/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
		}
            }
        }

        stage ("Push Docker Image"){
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub'){
                        dockerapp.push('latest')
			dockerapp.push("${env.BUILD_ID}")
                        
                    }
                }
            }
        }

        stage ("Deploy no Kubernetes"){
            environment {
	        tag_version = "${env.BUILD_ID}"   
	    }
	    steps {
		withKubeConfig([credentialsId: 'kube']){
                    sh 'sed -i "s/{{TAG}}/$tag_version/g" ./k8s/deployment.yaml'
		    sh 'sudo kubectl apply -f k8s/deployment.yaml'
		}
            }
        }
    }
}
