pipeline {
    agent any

    environment {
        CONTAIINER_NAME = "nestjs-app"
        IMAGE_NAME = "nesths-image"
        EMAIL = "sumityadav2579@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps[
                git branch: 'main', url: 'https://github.com/SumitYadav-new/CI-CD-Pipeline-Using-Jenkins-GitHub-Webhooks-Ubuntu-AWS-EC2-Docker.git'
            ]
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME ||
                    true
                    docker rm $CONTAINER_NAME || true
                    '''
            }
        }
        stage('Docker Container Run') {
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT}
                    --name $CONTAINER_NAME $IMAGE_NAME
                    '''
            }
        }
        stage('Send Email Notification') {
            steps {
                emailtext(
                    subject: "NestJS App Deployed
                    Succesfuly on EC2!",
                    body: "Your Nest JS app is Deployed!
                    http://http://56.228.22.232:${PORT}/",
                    to:  "${EMAIL}"
                )
            }
        }
    }
}