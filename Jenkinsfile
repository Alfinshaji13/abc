pipeline{
    agent any
    tools {
    maven 'maven_3_8_6'
    // scannerHome 'sonarqubeScanner-4.7.0'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Alfinshaji13/abc']]])
            }
        }
        
       stage ('Build') {
         steps {
              bat 'mvn clean install'
            }
         }
        stage('SonarQube analysis') {
        steps{
        withSonarQubeEnv('sonarqube-9.7.1') { 
         bat 'mvn clean verify sonar:sonar \
           -Dsonar.projectKey=abcd \
           -Dsonar.host.url=http://localhost:9000 \
           -Dsonar.login=sqp_13f3ad16768d553189a0e8098c6d5ee86443604c'
    }
        }
        }
       
    }
}
