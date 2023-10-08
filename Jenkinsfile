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
          // sh "docker tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
          // sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
          sh "docker logout"
        }
      }
    }
    stage("Deploy") {
      steps {
        sh "echo 'MYSQL_HOST=mysql
MYSQL_USER=luffy
MYSQL_PASSWORD=1234
MYSQL_DB=mr' > .env
        sh "docker-compose down && docker-compose up -d"
      }
    }
  }
}
