pipeline {
  agent {
    docker {
      image "node:lts-alpine3.9"
      args "--network skynet"
    }
  }
  stages {
    stage("Build") {
      steps {
        sh "apk add --no-cache mongodb"
        sh "chmod +x ./scripts/dropdb.sh"
        sh "npm install"
      }
    }
    stage("Test") {
      steps {
        sh "npm run test:ci"
      }
      post {
        always {
          junit "log/*.xml"
        }
      }  
    }
    stage("Production") {
      steps {
        input message: "Go to production? (Click 'Proceed' to continue)"
        sh "echo 'subindo em produção'"
      }
    }
  }
}
