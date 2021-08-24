pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh "docker build -f Dockerfile -t ${params.DOCKER_REPOSITORY} ."
                sh "echo ${params.DOCKER_REPOSITORY} > sysdig_secure_images"
            }
        }
        stage('Scanning Image') {
            steps {
            sysdig engineCredentialsId: 'sysdig-secure-api-credentials', name: 'sysdig_secure_images', inlineScanning: true
            }
        }
   }
}
