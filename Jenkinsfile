pipeline {
  agent any
  environment {
    TAG_NAME = 'my_app'
    S3_BUCKET = 'jenkins-bucket-11111111'
    BUILD_DIR = 'dist'
  }
  tools {
    nodejs 'Node JS'
  }
    
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/dhawal-901/jenkins-task-2.git'
      }
    }
    
    stage('Build React App') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }
    
    stage('Upload to S3') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'f0e8ab17-838c-4346-831e-a18c57a9575d']]) {
          sh '''
            aws s3 sync dist/ s3://$S3_BUCKET/ --region ap-south-1
            '''
        }
      }
    }
  }
}
