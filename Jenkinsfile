pipeline{
    agent any{
        stages{
            stage('Build'){
                step{
                  script{
                      echo"Building Docker Image"
                      def imageName = node-web-app
                      sh "docker build -t ${imageName} ."
                      echo"Docker Image built Successfully"
                    }
                  }
              }
          }
      }
  }
