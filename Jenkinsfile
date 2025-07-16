pipeline {
  agent any

  environment {
    ECR_REGISTRY = "964206357868.dkr.ecr.us-east-1.amazonaws.com"
    ECR_REPO = "node-app-repo"
    IMAGE_TAG = "latest"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/manitrpc/my-node-app.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh """
          docker build -t $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG .
        """
      }
    }

    stage('Push to ECR') {
      steps {
        sh """
          aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $ECR_REGISTRY
          docker push $ECR_REGISTRY/$ECR_REPO:$IMAGE_TAG
        """
      }
    }
  }
}
