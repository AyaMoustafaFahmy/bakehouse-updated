  
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
                sh "https://github.com/AyaMoustafaFahmy/bakehouse-updated"
               }
        } 
        
        stage(' login docker ') { 
            steps { 
                withCredentials([usernamePassword(credentialsId: 'dockerhub_id', passwordVariable: 'My_password', usernameVariable: 'ayamoustafa')]) {
                sh "docker login --username ayamoustafa --password ${My_password}"
                }
            } 
        }

        if (${params.CHOICE} == 'release'){
            sh ''
                docker build -t ayamoustafa/jenkins:$BUILD_NUMBER .
                docker docker push $registry
                ''

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
