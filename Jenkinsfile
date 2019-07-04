pipeline {
  agent {
    node {
      label 'master'
    }

  }
  stages {
    stage('echo') {
      steps {
        sh 'echo "test"'
      }
    }
    stage('git checkout') {
      steps {
        git(url: 'https://github.com/tmorozov/ci-workshop', branch: 'master', credentialsId: '7b9fe973-8c6d-47af-8052-cd7f26f81d54')
      }
    }
    stage('run app') {
      steps {
        dir(path: 'flask-app') {
          sh 'docker-compose up -d --build'
        }

      }
    }
    stage('stop app') {
      steps {
        dir(path: 'flask-app') {
          sh 'docker-compose down'
        }

      }
    }
  }
}