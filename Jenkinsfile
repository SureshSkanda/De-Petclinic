pipeline {
  agent any
  stages {
    stage('Commits detected') {
      steps {
        parallel(
          "Commits detected": {
            echo 'commits'
            
          },
          "Clean": {
            sh 'echo "data"'
            
          }
        )
      }
    }
    stage('Initialize') {
      steps {
        parallel(
          "Initialize": {
            echo 'echo "data"'
            
          },
          "mvn clean": {
            echo 'echo "data"'
            
          },
          "clone": {
            echo 'echo "data"'
            
          }
        )
      }
    }
    stage('end') {
      steps {
        echo 'echo "data"'
      }
    }
  }
}