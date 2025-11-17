pipeline{
   agent any
   environment{
         DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds)'
         DOCKER_HUB_USER = 'shilpakuntla'
         IMAGE_NAME = 'myapp' 
   } 
   stages
  {
     
      stage('Clone Repository'){
          steps{
             git branch: 'practice',
                 url:  'https://github.com/ShilpaKuntla/gs-rest-service'
          }
      }
     stage('Build Project'){
         steps{
            sh "mvn clean package -DskipTests"
         }
     }  
     stage('Build Docker Image'){
         steps{
            sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest ."
         }
     }
     stage('Login to Docker Hub'){
         steps{
            sh """
               echo "${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR}"
               --password -stdin
            """
         }
     }
     stage('Push Docker Image'){
         steps{
            sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
         }
     }
     post{
        always{
            sh 'docker logout'
        }
     } 
      
  }


}






