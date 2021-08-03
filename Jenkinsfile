pipeline { 
    environment { 
        registry = "ayamoustafa/jenkins:$BUILD_NUMBER" 
        registryCredential = 'dockerhub_id' 
        dockerImage = '' 
    }
    
    agent any 
    stages { 
        stage('Cloning Git') { 
            steps { 
                checkout scm
            }
        } 
        
        stage('Building image') { 
            steps { 
                script { 
                    sh "docker build -t ayamoustafa/jenkins:$BUILD_NUMBER ."
                    sh "docker login --username ayamoustafa --password ${my_docker_pass}"
                    //dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }


        stage('Deploy our image') { 
            steps { 
                script { 
//                     docker.withRegistry( '', registryCredential ) { 
//                         dockerImage.push() 
                    sh "docker push $registry"
                    
                 
                } 
            }
        } 

        
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 

    }
}
