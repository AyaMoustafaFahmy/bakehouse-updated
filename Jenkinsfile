  
pipeline { 
    environment { 
        registry = "ayamoustafa/jenkins:$BUILD_NUMBER" 
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
              script{
                sh "https://github.com/AyaMoustafaFahmy/bakehouse-updated.git"
              }
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
            if (${params.CHOICE} == 'release'){
                sh " docker build -t ayamoustafa/jenkins:$BUILD_NUMBER ."
                sh "  docker docker push $registry "

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
