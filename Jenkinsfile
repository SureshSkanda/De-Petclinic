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
        sh '''mvn findbugs:check
mvn test'''
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
    stage('Sonar Analysis') {
      steps {
        script {
          git '/var/lib/jenkins/workspace/Skanda_De-Petclinic_brave-TVG6UIEQISBJB4V4QVU2J4RG5U7SRNCIWRDZXZRLTNJR3FVWONYA'
          def scannerHome = tool 'Sonarscanner';
          withSonarQubeEnv {
            sh "${scannerHome}bin/sonar-runner"}
          }
          
        }
      }
    }
  }