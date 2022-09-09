pipeline {
        agent any 
        environment{
        git_TKN=credentials('git_TKN')
           }

        stages {
          stage('pull-code') { 
            steps {
                git credentialsId: 'github_TKN', url: 'https://github.com/vishalsontakke26/Assessment-knx-devops-microservice-test.git'
                 }
                     }
            
        stage('Build') { 
            steps {
             sh 'sudo docker build -t test1:v2 .'
            }
              }
          
         stage('push') { 
            steps {
              sh 'sudo docker tag test1:v2 vishalsontakke/test1:v2'
              sh'sudo docker login -u vishalsontakke --password $git_TKN'
              sh'sudo docker push vishalsontakke/test1:v2'

            }
          }
          stage('pull & deploy') { 
            steps {
             
              sh'sudo docker pull vishalsontakke/test1:v2'
              sh'sudo docker run -d -p 80:80 vishalsontakke/test1:v2'

            }
          }
          
      } 
    }
