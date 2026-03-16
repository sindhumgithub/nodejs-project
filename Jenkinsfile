// pipeline {
//     agent any 
//     environment {
//         AWS_REGION = 'us-east-1'
//         ECR_REPO = '324827177100.dkr.ecr.us-east-1.amazonaws.com/nodejs-eks-app'
//     }

//     stages {
//         stage ('Clone the Github Repo') {
//             steps {
//                 git 'https://github.com/sindhumgithub/nodejs-project.git'
//             }
//         }

//         stage ('Build docker Image') {
//             steps {
//                 sh 'docker build -t nodejs-eks-app .'
//             }
//         }

//         stage('Login to AWS') {
//             steps {
//                 withCredentials([string(credentialsId: 'AWS-SecretKey', variable: 'AWS_SECRET')]) {
//                     sh '''
//                     export AWS_SECRET_ACCESS_KEY=$AWS_SECRET
//                     '''
//                 }
//             }
//         }

//         stage ('Push to ECR') {
//             steps {
//                 sh '''
//                 aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO
//                 docker tag nodejs-eks-app:latest $ECR_REPO:latest
//                 docker push $ECR_REPO:latest
//                 '''
//             }
//         }

//     }
// }

// pipeline {
//     agent any

//     environment {
//         AWS_REGION = 'us-east-1'
//         ECR_REPO = '324827177100.dkr.ecr.us-east-1.amazonaws.com/nodejs-eks-app'
//     }

//     stages {

//         stage('Clone Github Repo') {
//             steps {
//                 git 'https://github.com/sindhumgithub/nodejs-project.git'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 sh 'docker build -t nodejs-eks-app .'
//             }
//         }

//         stage('Login to AWS ECR') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'aws-jenkins'
//                 ]]) {
//                     sh '''
//                     aws ecr get-login-password --region $AWS_REGION | \
//                     docker login --username AWS --password-stdin $ECR_REPO
//                     '''
//                 }
//             }
//         }

//         stage('Push Image to ECR') {
//             steps {
//                 sh '''
//                 docker tag nodejs-eks-app:latest $ECR_REPO:latest
//                 docker push $ECR_REPO:latest
//                 '''
//             }
//         }

//     }
// }


pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        ECR_REGISTRY = '324827177100.dkr.ecr.us-east-1.amazonaws.com'
        ECR_REPO = 'nodejs-eks-app'
        IMAGE_TAG = 'latest'
    }

    stages {

        stage('Clone GitHub Repo') {
            steps {
                git 'https://github.com/sindhumgithub/nodejs-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $ECR_REPO:$IMAGE_TAG .'
            }
        }

        stage('Login to AWS ECR') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-jenkins'
                ]]) {
                    sh '''
                    aws ecr get-login-password --region $AWS_REGION | \
                    docker login --username AWS --password-stdin $ECR_REGISTRY
                    '''
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh '''
                docker tag $ECR_REPO:$IMAGE_TAG $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
                '''
            }
        }

        stage('Push Image to ECR') {
            steps {
                sh '''
                docker push $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
                '''
            }
        }

    }
}