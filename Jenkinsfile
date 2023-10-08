pipeline {
  agent any
  stages {
    
    stage("Code") {
      steps {
        git url: "https://github.com/MohammedAtique/two-tier-flask-app", branch: "master"
      }
    }
    stage("Build && Test") {
      steps {
        sh "docker build . -t two-tier-flask-app"
      }
    }
    stage("Push to dockerHub") {
      steps {
        withCredentials([usernamePassword(credentialsId:"dockerHub", passwordVariable:"dockerHubPass", usernameVariable:"dockerHubUser")]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
          sh "docker tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
          sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
        }
      }
    }
    stage("Deploy") {
      steps {
        // sh "docker-compose down && docker-compose up -d"
        sh "docker run -d -p 5000:5000 two-tier-flask-app"
      }
    }
  }
}
