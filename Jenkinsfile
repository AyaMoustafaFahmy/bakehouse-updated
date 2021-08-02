pipeline { 
    environment { 
        registry = "ayamoustafa/jenkins" 
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

    }
}
