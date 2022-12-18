pipeline {
    agent any
  
  environment {
    // Adjust variables below
    IMAGE_NAME = "docker.io/your_dockerhub_username/webapp"
    TAG = sh (script: "date +%y%m%d%H%M", returnStdout: true).trim()
  }
  
  stages {
    stage('Preparation') {
      steps {
        sh "echo App Version = $TAG"
      }
    }

    stage('Test') {
      steps {
        sh "html5validator html/index.html"
      }
      post {
        success {
           echo "Test Successful"
        }
        failure {
           echo "Test Failed"
        }
      }
    }
    
    stage("Build & Push Image"){
      steps{
        script {
          dockerImage = docker.build("$IMAGE_NAME:$TAG")
          dockerImage.push()
        }
      }
      post {
        success {
           echo "Build & Push Successful"
        }
        failure {
           echo "Build & Push Failed"
        }
      }
    }
  }
}
