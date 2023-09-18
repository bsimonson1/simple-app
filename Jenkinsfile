pipeline {
    agent any
    tools {nodejs "node"}
    environment {
    imageName = benjayyy/jenkins_ufl
    dockerCredentialsName='dockerhub-creds'
    dockerImage = ''
    }
    stages {
        stage('Environment') {
            steps {
                echo "Branch: ${env.BRANCH_NAME}"
                sh 'docker -v'
            }
        }
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build benjayyy/jenkins_ufl
                }
            }
        }
        stage('Deploy Image') {
            steps{
                script {
                    docker.withRegistry('https://registry.hub.docker.com',
dockerCredentialsName
) {
            dockerImage.push("${env.BUILD_NUMBER}")
            dockerImage.push("latest")
                }
                }
            }
        }
    }
}