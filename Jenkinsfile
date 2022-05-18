pipeline {
   agent any

   environment {
 
     SERVICE_NAME = "fleetman-webapp"
     ECR_URI = "738942673819.dkr.ecr.us-east-2.amazonaws.com/fleetman-webapp"
     REPOSITORY_TAG ="${ECR_URI}:${BUILD_ID}"
   }

   stages {
      
      stage('Build') {
         steps {
            sh 'echo No build required for Webapp.'
         }
      }

      stage('Build and Push Image') {
         steps {
           // sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 738942673819.dkr.ecr.us-east-2.amazonaws.com'
            
           sh 'docker image build -t ${REPOSITORY_TAG} .'
           sh 'docker push ${REPOSITORY_TAG}'
         }
      }

      stage('Deploy to Cluster') {
          steps {
            sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
          }
      }
   }
}
