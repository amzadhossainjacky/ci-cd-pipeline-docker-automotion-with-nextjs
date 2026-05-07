pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app-container"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "amzadhossain1922@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps{
                git branch: 'master', url: 'https://github.com/amzadhossainjacky/ci-cd-pipeline-docker-automotion-with-nextjs'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }
        stage('Docker Container Run') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }
        // stage('Send Email Notification') {
        //     steps {
        //        emailext(
        //         subject: "NestJS App Deployed Successfully on Personal Server!",
        //         body: "Your Nest JS app is Deployed! http://114.130.69.222:${PORT}/",
        //         to: "${EMAIL}"
        //        )
        //     }
        // }

    }
}