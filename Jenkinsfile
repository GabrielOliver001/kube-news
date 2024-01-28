pipeline {
    agent any 
    
    stages {
        stage ("Build Docker Image"){
            steps {
                script {
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
		    sh 'kubectl apply -f k8s/deployment.yaml'
		}
            }
        }
    }
}
