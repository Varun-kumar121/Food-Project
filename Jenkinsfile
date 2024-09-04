pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/Varun-kumar121/Food-Project.git'
        S3_BUCKET = 'food-project-deployment-bucket'
        APPLICATION_NAME = 'FoodProjectApp'
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
                // Include build steps, such as npm build or Maven build, if necessary
                echo 'Building application...'
            }
        }
        stage('Package') {
            steps {
                sh 'zip -r Food-Project.zip *'
            }
        }
        stage('Upload to S3') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials-id') {
                    s3Upload(file: 'Food-Project.zip', bucket: "${S3_BUCKET}", path: "Food-Project.zip")
                }
            }
        }
        stage('Deploy to EC2') {
            steps {
                withAWS(region: "${AWS_REGION}", credentials: 'aws-credentials-id') {
                    codedeployDeploy(
                        applicationName: "${APPLICATION_NAME}",
                        deploymentGroupName: "${DEPLOYMENT_GROUP_NAME}",
                        s3Location: [
                            bucket: "${S3_BUCKET}",
                            key: "Food-Project.zip",
                            bundleType: 'zip'
                        ]
                    )
                }
            }
        }
    }
}
