pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/laxmi916/node-docker-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t node-docker-app:${BUILD_NUMBER} .
                docker tag node-docker-app:${BUILD_NUMBER} laxmi916/node-docker-app:${BUILD_NUMBER}
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push laxmi916/node-docker-app:${BUILD_NUMBER}'
            }
        }
        
        stage('Deployment of nodeapp'){
             steps{
                 sh '''
                     kubectl --apply -f k8/k8deployment.yml
                 '''
             }
       }
       
       stage('Expose Service'){
              steps{
                   sh '''
                      kubectl --apply -f k8/k8Service.yml
                   '''
             }
      }
      
     

    }
}
