pipeline {
    agent any
    environment {
        HTTP_PROXY = 'http://10.219.244.193:3128'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh "sudo docker build --build-arg http_proxy=http://10.219.244.193:3128 HTTP_PROXY=http://10.219.244.193:3128 -f Dockerfile -t ${params.DOCKER_REPOSITORY} ."
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
