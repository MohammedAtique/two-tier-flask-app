pipeline {
  agent any
  stages {
    stage('Code') {
      steps {
        echo "Code cloned"
      }
    }
    stage('Build && Test') {
      steps {
        echo "Build and test"
      }
    }
    stage('Push to dockerHub') {
      steps {
        echo "Pushing image to dockerHub"
      }
    }
    stage('Deploy') {
      steps {
        echo "Deployment successfull"
      }
    }
  }
}
