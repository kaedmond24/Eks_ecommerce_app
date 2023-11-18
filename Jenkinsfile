pipeline {
  agent {label 'awsDeploy'}
  environment{
      DOCKERHUB_CREDENTIALS = credentials('kaedmond24-dockerhub')
      }

    stages {
     
      stage ('Build') {
        steps {
          dir('backend'){
            sh 'sudo docker build -t kaedmond24/d9backend .'
          }
        }
      
       }
   }
     stage ('Login') {
        steps {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
      
        }
   }

     stage ('Push') {
        steps {
          dir('backend'){
            sh 'sudo docker push kaedmond24/d9backend'
          }
        }
       
       }
    }

      stage ('Backend deployment') {
        agent {label 'awsDeploy2'}
        steps {
          dir('backend'){
            sh 'kubectl apply -f deployment.yaml'
          }
        }
       
     }
  }

     stage ('Backend service') {
        agent {label 'awsDeploy2'}
        steps {
          dir('backend'){
            sh 'kubectl apply -f service.yaml '
          }
        }
        
      }
    }
