pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo "Building Docker Image"
                    def imageName = "node-web-app"  // Enclose the image name in double quotes
                    sh "docker build -t ${imageName} ."
                    echo "Docker Image built Successfully"  // Add space before the string
                }
            }
        }
    }
}

