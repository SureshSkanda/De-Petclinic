pipeline {
  agent any
  stages {
    stage('Commits Detected') {
      steps {
        echo 'New commits detected'
      }
    }
    stage('Initialize') {
      steps {
        parallel(
          "Initialize": {
            echo 'Initialising..'
            
          },
          "Workspace clean": {
            sh 'mvn clean'
            
          },
          "Code Checkout": {
            echo 'Checking out code'
            
          }
        )
      }
    }
    stage('Maven Invoke') {
      steps {
        echo 'maven invoke'
      }
    }
    stage('Sanity Check') {
      steps {
        sh 'mvn findbugs:check'
      }
    }
    stage('Unit Test') {
      steps {
        parallel(
          "Unit Test": {
            sh 'mvn test'
            
          },
          "Junit": {
            junit '**/target/surefire-reports/TEST-*.xml'
            
          }
        )
      }
    }
    stage('Build') {
      steps {
        sh 'mvn package'
      }
    }
  }
}