pipeline {
    environment {
        registry = "8if8troin6i4rv2p/capstone-v3"
        registryCredential = 'dockerhub-user'
        dockerImage = ''
        }
    agent any

    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/SamirduUd/capstone-v3.git'
            }
    }

        stage('Building our image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                    }
                }
            }
        }

        stage('Cleaning up') {
            steps{
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}