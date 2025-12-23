pipeline {
  agent any

  stages {
    stage('Clone Code') {
      steps {
        echo 'Code already cloned by Jenkins'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t it-website .'
      }
    }

    stage('Run Docker Container') {
      steps {
        sh '''
        docker stop it-website || true
        docker rm it-website || true
        docker run -d -p 80:80 --name it-website it-website
        '''
      }
    }
  }
}
