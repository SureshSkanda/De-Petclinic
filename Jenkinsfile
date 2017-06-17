pipeline {
  agent any
  stages {
    stage('Commits detected') {
      steps {
        parallel(
          "Commits detected": {
            echo 'commits'
            
          },
          "Workspace Clean": {
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
          "Checkout": {
            echo 'echo "data"'
            
          },
          "Maven Invoke": {
            echo 'echo "data"'
            
          }
        )
      }
    }
    stage('res1') {
      steps {
        sh 'sleep 10s'
      }
    }
    stage('res2') {
      steps {
        sh 'sleep 10s'
      }
    }
    stage('res3') {
      steps {
        sh 'sleep 10s'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn package'
      }
    }
    stage('res4') {
      steps {
        sh 'sleep 10s'
      }
    }
    stage('res5') {
      steps {
        sh 'sleep 10s'
      }
    }
    stage('Sonar Analysis') {
      steps {
        script {
          git '/var/lib/jenkins/workspace/Skanda_De-Petclinic_develop-K7G46OPVOWKZXUEVYDGNHT4WGZ7ICO7ZFDXERX3VMW5O5JUOSTDQ'
          def scannerHome = tool 'Sonarscanner';
          withSonarQubeEnv {
            sh "${scannerHome}bin/sonar-runner"}
          }
          
        }
      }
      stage('Sonar Qualitygate') {
        steps {
          waitForQualityGate()
        }
      }
      stage('Nexus Archive') {
        steps {
          script {
            nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: '/var/lib/jenkins/workspace/Skanda_De-Petclinic_develop-K7G46OPVOWKZXUEVYDGNHT4WGZ7ICO7ZFDXERX3VMW5O5JUOSTDQ/target/petclinic.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '35.154.15.190:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '4.0.${BUILD_NUMBER}'
          }
          
        }
      }
      stage('Deploy env. with Chef') {
        steps {
          parallel(
            "Deploy Env. with Chef": {
              sh 'sleep 5s'
              script {
                
              }
              
              
            },
            "Cookbooks uploading": {
              sh 'sleep 5s'
              script {
                sh 'cat /var/lib/jenkins/pwd | sudo -S su - ubuntu -c "/home/ubuntu/jendepscripts/d-ssh.sh"'
              }
              
              
            }
          )
        }
      }
      stage('Chef Server Spinup') {
        steps {
          parallel(
            "Chef Server Spinup": {
              sh 'sleep 5s'
              script {
                sh 'cat /var/lib/jenkins/pwd | sudo -S su - ubuntu -c "/home/ubuntu/jendepscripts/d-cookbookupload.sh"'
              }
              
              
            },
            "Checking Env. Nodes": {
              sh 'sleep 5s'
              
            }
          )
        }
      }
      stage('Deployment initiation') {
        steps {
          sh 'sleep 5s'
        }
      }
      stage('Binary Distribution') {
        steps {
          parallel(
            "Binary Distribution": {
              sh 'sleep 5s'
              
            },
            "Deploying to QA": {
              sh 'sleep 5s'
              script {
                sh 'cat /var/lib/jenkins/pwd | sudo -S su - ubuntu -c "/home/ubuntu/jendepscripts/d-chefclientspin.sh"'
              }
              
              
            },
            "Deploying to Pre-Prod": {
              sh 'sleep 5s'
              
            }
          )
        }
      }
    }
  }