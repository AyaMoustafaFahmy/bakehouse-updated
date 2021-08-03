pipeline {
    agent any
    stages {
        stage('pull image from dockerhub') {
            steps {
            	withCredentials([usernameColonPassword(credentialsId: 'dockerhub_id', variable: 'prod')]) {
			       
			sh 'docker pull ayamoustafa/jenkins'

			}
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
