pipeline {
    agent any

    tools {
        maven "maven_3_9_9"
    }

    stages {
        stage('Build') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ZXAfromOVERWORLD/task2']])                
                sh "mvn clean install"
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t task/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u javatechie -p ${dockerhubpwd}'

                    }
                   sh 'docker push javatechie/devops-integration'
                }
            }
        }
    }
}
