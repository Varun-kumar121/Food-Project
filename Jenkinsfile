pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/Varun-kumar121/Food-Project.git'
        S3_BUCKET = 'food-project-deployment-bucket'
        APPLICATION_NAME = 'MyWeb'
        DEPLOYMENT_GROUP_NAME = 'FoodProjectDeploymentGroup'
        AWS_REGION = 'us-east-2'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: "${REPO_URL}", branch: 'master'
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
                // Include your build commands here, e.g., npm install, mvn package, etc.
            }
        }
        stage('Package') {
            steps {
                sh 'zip -r Food-Project.zip *'
            }
        }
        stage('Upload to S3') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-credentials-id']]) {
                    sh '''
                    aws s3 cp Food-Project.zip s3://${S3_BUCKET}/Food-Project.zip --region ${AWS_REGION}
                    '''
                }
            }
        }
        stage('Deploy to EC2') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-credentials-id']]) {
                    sh '''
                    aws deploy create-deployment \
                        --application-name ${APPLICATION_NAME} \
                        --deployment-group-name ${DEPLOYMENT_GROUP_NAME} \
                        --s3-location bucket=${S3_BUCKET},key=Food-Project.zip,bundleType=zip \
                        --region ${AWS_REGION}
                    '''
                }
            }
        }
    }
}
