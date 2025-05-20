pipeline {
    agent any

    environment{
        dockerimagename = "namratha3/dev-nodeapp"
        registryCredential = 'dockerhublogin'
    }
    stages {
        stage('Checkout Source'){
            steps{
                git 'https://github.com/Namrathaaaaaa/node-app-devops.git'
            }
        }

        stage('Build image'){
            steps{
                script{
                    dockerImage = docker.build(dockerimagename)
                }
            }
        }

        stage('Pushing Image'){
            steps{
                script{
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential){
                      dockerImage.push("latest")
                    }
                }
            }
        }
        stage('Deploying app to kubernetes'){
            steps{
                script{
                    kubernetesDeploy(configs: "deploymentservice.yaml", kubconfigId: "kubernetes")
                }
            }

        }
    }
}