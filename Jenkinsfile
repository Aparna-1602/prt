pipeline {
   environment {
     git_url = "https://github.com/Aparna-1602/Website-PRT-ORG.git"
     git_branch = "master"
   }

  agent any
 
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: 'f5de3230-35f9-4633-8ece-1941022004bb', branch: "${git_branch}", url: "${git_url}"
       
      }
     }
     
     stage('Docker Image Build') {     
        steps {
              sh 'sudo docker build -t myjava-image . '
               }
             }
        stage('Docker image push') {
           steps {
                 withCredentials([usernamePassword(credentialsId: 'e110bfc4-0118-40ec-b084-939a4342b0ae', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag myimage aparna078/myimage:test"
                 sh "sudo docker image push aparna078/myimage:test" 
               } 
             }  
          }
      stage('Deploy app') {
         steps {
            sh 'kubectl apply -f app-deploy.yaml'
            sh 'kubectl apply -f app-svc.yaml'
         }
      }
    }

  
  }
