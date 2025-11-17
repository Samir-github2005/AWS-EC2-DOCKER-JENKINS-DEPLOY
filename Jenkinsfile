pipeline{
    agent any

    environment{
        CONTAINER_NAME="nestjs-app"
        IMAGE_NAME="nestjs-image"
        EMAIL="bhaktasamir11042005@gmail.com"
        PORT="3000"
    }

    stages{
        stage('clone repo'){
            steps{
                git branch: 'main', url: 'https://github.com/Samir-github2005/AWS-EC2-DOCKER-JENKINS-DEPLOY.git'
            }
        }

        stage('build docker image'){
            steps{
                sh 'docker build -t ${IMAGE_NAME} .'
            }
        }

        stage('stop and remove prev container'){
            steps{
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('docker container run'){
            steps{
                sh '''
                    docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}
                '''
            }
        }

        stage('send email notifications'){
            steps{
                emailext(
                    subject:"nest app deployed on AWS-ec2",
                    body:"your app is deployed http://16.170.157.59:${PORT}/",
                    to:"${EMAIL}"
                )
            }
        }
    }
}