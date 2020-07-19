pipeline {
  agent {
    docker {
      image "node:12-alpine"
    }
  }
  stages {
    stage("Build") {
      steps {
        // sh "apk add --no-cache mongodb"
        sh "echo 'http://dl-cdn.alpinelinux.org/Alpine/v3.6/main' >> /etc/apk/repositories"
        sh "echo 'http://dl-cdn.alpinelinux.org/Alpine/v3.6/community' >> /etc/apk/repositories"
        sh "apk update"
        sh "apk add mongodb=3.4.4-r0"
        sh "chmod +x ./scripts/dropdb.sh"
        sh "npm install"
      }
    }
    stage("Test") {
      steps {
        sh "npm run test:ci"
      }
    }
  }
}