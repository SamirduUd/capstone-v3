pipeline {
    environment {
        registry = "8if8troin6i4rv2p/capstone-v3"
        dockerCredential = 'dockerhub-user'
        dockerImage = ''
        ROLE = 'blue'
        awsRepository = "206893810529.dkr.ecr.us-east-2.amazonaws.com/capstone-v3"
        awsRegion = "us-east-2"
        awsZone1 = "us-east-2a"
        awsZone2 = "us-east-2b"
        awsCredential = 'aws-key'
        }
    
    agent any

    stages {
        stage('Cloning Capstone Project from Github') {
            steps {
                git 'https://github.com/SamirduUd/capstone-v3.git'
            }
        }

        stage('Lint HTML') {
			steps {
				sh 'tidy -q -e *.html'
			}
		}

        stage('Building Docker Image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Push Docker Image') {
            steps{
                script {
                    docker.withRegistry( '', dockerCredential ) {
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


