pipeline {
  agent {
    node {
      label 'slave1'
    }

  }
  stages {
    stage('git checkout') {
      steps {
        git(url: 'https://github.com/tmorozov/ci-workshop', branch: 'master', credentialsId: '7b9fe973-8c6d-47af-8052-cd7f26f81d54')
      }
    }
    stage('tests') {
      steps {
        dir(path: 'flask-app') {
          sh '''docker-compose down
docker-compose build flask-app
docker-compose run flask-app pytest -v --junit-xml=/var/opt/junit-report/report.xml
docker-compose down
'''
        }

      }
    }
    stage('Archive test results') {
      steps {
        junit 'flask-app/junit-report/report.xml'
      }
    }
    stage('cleanup') {
      steps {
        sh 'sudo rm -rf flask-app/junit-report'
      }
    }
  }
}