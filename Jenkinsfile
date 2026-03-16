pipeline {
    agent any 
    environment {
        AWS_REGION = 'us-east-1'
        ECR_REPO = '324827177100.dkr.ecr.us-east-1.amazonaws.com/nodejs-eks-app'
    }

    stages {
        stage ('Clone the Github Repo') {
            steps {
                git 'https://github.com/sindhumgithub/nodejs-project.git'
            }
        }

        stage ('Build docker Image') {
            steps {
                sh 'docker build -t nodejs-eks-app .'
            }
        }

        stage ('Push to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
                docker tag nodejs-eks-app:latest $ECR_REPO:latest
                docker push $ECR_REPO:latest
                '''
            }
        }

    }
}