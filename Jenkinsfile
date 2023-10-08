pipeline {
  agent any
  stages {
    stage('Code') {
      steps {
        git url: 'https://github.com/MohammedAtique/two-tier-flask-app', branch: 'master'
      }
    }
    stage('Build && Test') {
      steps {
        sh 'docker build . -t two-tier-flask-app'
      }
    }
    stage('Push to dockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId:'dockerHub', passwordVariable:'pass', usernameVariable:'user')]) {
          sh 'docker login -u ${env.user} -p ${env.pass}'
        }
      }
    }
    stage('Deploy') {
      steps {
        echo "Deployment successfull"
      }
    }
  }
}
