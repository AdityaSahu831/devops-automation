pipeline{
    agent any
    tools {
        maven 'maven 3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AdityaSahu831/devops-automation']])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                  bat 'docker build -t sahu00157/devops-integration .'
                }
            }
        }
        stage('Push Docker Image to Docker Hub'){
            steps{
                script{
                     bat 'docker login -u sahu00157 -p ggits0206'
                     bat 'docker push sahu00157/devops-integration'
                }
            }
        }
        stage('Deploy to K8S'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
    }
}