pipeline {
    agent any

    environment {
        dockerimagename = "namratha3/dev-nodeapp"
        registryCredential = 'dockerhublogin'
    }

    stages {
        stage('Checkout Source') {
            steps {
                git branch: 'main', url: 'https://github.com/Namrathaaaaaa/node-app-devops.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build(dockerimagename)
                }
            }
        }

        stage('Push Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
                        dockerImage.push("latest")
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubernetesDeploy(
                        configs: "deploymentservice.yaml",
                        kubeconfigId: "kubernetes"
                    )
                }
            }
        }
    }
}
