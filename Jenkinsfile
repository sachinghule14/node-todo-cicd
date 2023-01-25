pipeline {
    agent { label 'master' }
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/sachinghule14/node-todo-cicd.git', branch: 'master' 
            }
        }
        stage('Build and Test'){
            steps{
                bat 'docker build . -t trainwithshubham/node-todo-test:latest'
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	     bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 bat 'docker push trainwithshubham/node-todo-test:latest'
                }
            }
        }
        stage('Deploy'){
            steps{
                bat "docker-compose down && docker-compose up -d"
            }
        }
    }
}
