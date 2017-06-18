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
        parallel(
          "Maven Invoke": {
            echo 'maven invoke'
            
          },
          "Sanity Check": {
            sh '''mvn findbugs:check
mvn test'''
            
          },
          "Unit Tests": {
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
          git '/var/lib/jenkins/workspace/shSkanda_De-Petclinic_brave-TVG6UIEQISBJB4V4QVU2J4RG5U7SRNCIWRDZXZRLTNJR3FVWONYA'
          def scannerHome = tool 'Sonarscanner';
          withSonarQubeEnv {
            sh "${scannerHome}bin/sonar-runner"}
          }
          
        }
      }
      stage('Nexus Archive') {
        steps {
          script {
            nexusArtifactUploader artifacts: [[artifactId: 'spring-petclinic', classifier: '', file: '/var/lib/jenkins/workspace/shSkanda_De-Petclinic_brave-TVG6UIEQISBJB4V4QVU2J4RG5U7SRNCIWRDZXZRLTNJR3FVWONYA/target/petclinic.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '35.154.15.190:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-releases', version: '5.0.${BUILD_NUMBER}'
          }
          
        }
      }
      stage('Chefserver Spinup') {
        steps {
          script {
            
          }
          
        }
      }
    }
  }