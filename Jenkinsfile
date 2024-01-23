pipeline {
  agent any

  parameters {
    string(name: 'IMAGE_NAME', defaultValue: 'dashboard', description: 'Docker image name')
    string(name: 'DOCKERHUB_USERNAME', defaultValue: 'ash0semlali', description: 'Docker Hub username')
  }

  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }

  stages {
    stage('Checkout code') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh "docker build -t ${params.IMAGE_NAME}:latest ."
      }
    }

    stage('Test') {
      steps {
        echo "test passed"
      }
    }

    stage('Push Images to Docker Hub') {
      steps {
        sh 'echo %DOCKERHUB_CREDENTIALS_PSW%| docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
        sh "sudo docker tag ${params.IMAGE_NAME}:latest ${params.DOCKERHUB_USERNAME}/${params.IMAGE_NAME}:latest"
        sh "sudo docker push ${params.DOCKERHUB_USERNAME}/${params.IMAGE_NAME}:latest"
      }
    }

    stage('Cleanup') {
        steps {
          sh 'sudo docker logout'
        }
      }
  }
}
