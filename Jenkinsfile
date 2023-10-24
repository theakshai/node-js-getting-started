pipeline {
    agent any
    environment {
        IMAGE_NAME = "node-web-app"
        REGION = "us-east-1"
    }
    stages {
        stage('Build') {
            steps {
                script {
                    sh "docker build -t ${env.IMAGE_NAME} ."
                    echo "Docker Image built Successfully"
            }
        }
        }
        stage('Pushing Docker Image to ECR'){
            steps{
                script{
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-key', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                        sh "aws ecr-public get-login-password --region ${env.REGION} | docker login --username AWS --password-stdin public.ecr.aws/s5o7d0z2"
                        sh "docker tag ${env.IMAGE_NAME}:latest public.ecr.aws/s5o7d0z2/aws-jenkins-ecr:latest"
                        sh "docker push public.ecr.aws/s5o7d0z2/aws-jenkins-ecr:latest"
                        echo "Docker Image successfully pushed to ECR"
                    }

                  }
              }
          }
          stage('Removing Docker Images from local'){
              steps{
                  script{
                        echo "Removing Docker Containers"
                        sh "docker rm -f \$(docker ps -q)"
                        echo "Removing Docker Images"
                        sh "docker rmi --force \$(docker images -q)"

                    }
                }
            }

    }
}
