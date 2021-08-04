  
pipeline { 
    environment { 
        registry = "ayamoustafa/jenkins" 
        registryCredential = 'dockerhub_id' 
        dockerImage = '' 
    }
    agent any 
        parameters{
        choice(name:'BRANCH',choices:['release','dev','prod','test'])
    }

    stages { 

        stage('Cloning Git') { 
            steps { 
                git 'https://github.com/AyaMoustafaFahmy/bakehouse-updated.git'
            }
        } 
        
        stage(' login docker ') { 
            steps { 
                withCredentials([usernamePassword(credentialsId: 'dockerhub_id', passwordVariable: 'My_password', usernameVariable: 'ayamoustafa')]) {
                sh "docker login --username ayamoustafa --password ${My_password}"
                }
            } 
        }
      
      
      stage(' Release ') {
        steps {
          script {
            if (params.CHOICE == 'release'){
                sh " docker build -t ayamoustafa/jenkins:$BUILD_NUMBER ."
                sh "  docker docker push  ayamoustafa/jenkins:$BUILD_NUMBER"

            }
          }
        }
      }
      
      stage('dev'){
            steps{
                scripts{
                    if (params.CHOICE == 'release'){
                        sh " docker pull ayamoustafa/jenkins:$BUILD_NUMBER ."
                        sh " kubectl apply -f namespace.yaml"
                        sh " kubectl apply -f deploy.yaml"
                        sh " kubectl apply -f service.yaml"
                    }
                }
            }
        }
    }
}

//         script { 

// //                     dockerImage = docker.build registry + ":$BUILD_NUMBER" 
//          }   


//         stage('Deploy our image') { 
//             steps { 
//                 script { 
// //                     docker.withRegistry( '', registryCredential ) { 
// //                         dockerImage.push() 
// //                     }
//                     sh "docker push $registry"
                 
//                 } 
//             }
//         } 

//     }
// }
