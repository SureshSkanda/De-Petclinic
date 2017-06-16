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
        parallel(
          "sonar": {
            script {
              git '/var/lib/jenkins/workspace/Skanda_De-Petclinic_develop-K7G46OPVOWKZXUEVYDGNHT4WGZ7ICO7ZFDXERX3VMW5O5JUOSTDQ'
              def scannerHome = tool 'Sonarscanner';
              withSonarQubeEnv {
                sh "${scannerHome}bin/sonar-runner"}
              }
              
              
            },
            "Junit": {
              junit '**/target/surefire-reports/TEST-*.xml'
              
            }
          )
        }
      }
      stage('Nexus Archive') {
        steps {
          script {
            nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: '/var/lib/jenkins/workspace/Skanda_De-Petclinic_develop-K7G46OPVOWKZXUEVYDGNHT4WGZ7ICO7ZFDXERX3VMW5O5JUOSTDQ/target/petclinic.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '35.154.15.190:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '4.0.${BUILD_NUMBER}'
          }
          
        }
      }
    }
  }