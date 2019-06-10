pipeline {
    agent any
    environment {
        DOCKER = credentials('docker-repository-credentials')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh "sudo docker build -f Dockerfile -t schofr/cronagent ."
            }
        }
        stage('Push Image') {
            steps {
                sh "sudo docker login --username ${DOCKER_USR} --password ${DOCKER_PSW}"
                sh "sudo docker push schofr/cronagent"
                sh "echo docker.io/schofr/cronagent > sysdig_secure_images"
            }
        }
        stage('Scanning Image') {
            steps {
                sysdigSecure 'sysdig_secure_images'
            }
        }
   }
}
