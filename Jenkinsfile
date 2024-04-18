pipeline {
    agent any
 
    stages {
        stage('Cloniing') {
            steps {
                echo 'Cloining the code from the github repository.'
                git 'https://github.com/Mayur-tiwari/star-agile-insurance-project.git'

            }
        }
        
        
        stage('Building') {
            steps {
                echo 'Building the given code by using maven'
                sh 'mvn install'
            }
            
        }
        
        
       stage('docker-image') {
           steps {
                echo 'creating an image using docker'
                sh 'sudo docker build -t mayurtiwari/insurance-img .'
           }

       }
       
        
       stage('Pushing') {
           steps {
               echo 'pushing that image to the DockerHub'
               withCredentilas([usernamePassword(credentialsId: 'Docker-pass', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                  sh 'sudo docker login -u ${env.USERNAME} -p ${env.PASSWORD}'
                  sh 'sudo docker push mayurtiwari/insurance-img'
               }
            }

         }
        
        stage('Deploying') {
            steps {
                echo 'Deploying that application to the production server'
                sh 'sudo ansible-playbook /home/ubuntu/Insurence-project/playbook.yaml'
            }
        }
    }
}
