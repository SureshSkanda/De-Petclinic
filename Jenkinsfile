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
    stage('build') {
      steps {
        echo 'echo "data"'
        sh 'mvn package'
      }
    }
    stage('sonar') {
      steps {
        script {
          git '/var/lib/jenkins/workspace/CI-CD/DewithChef/'
          def scannerHome = tool 'Sonarscanner';
          withSonarQubeEnv {
            sh "${scannerHome}bin/sonar-runner"}
          }
          
        }
      }
    }
  }