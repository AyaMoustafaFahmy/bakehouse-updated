pipeline {
    agent any
    stages {
        stage('pull image from dockerhub') {
            steps {		
	                sh "docker login --username ayamoustafa --password ${my_docker_pass}"
			sh 'docker pull ayamoustafa/jenkins:$BUILD_NUMBER'

			}
            }
        stage("deploy the k8s"){
        	steps{
        		sh "kubectl apply -f namespace.yaml"
        		sh "kubectl apply -f deploy.yaml"
        		sh "kubectl apply -f service.yaml"
        	}

        }
    }
}
