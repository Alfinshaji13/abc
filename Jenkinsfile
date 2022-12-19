pipeline{
    agent any
    tools {
    maven 'maven_3_8_6'
    scannerHome 'sonarqubeScanner-4.7.0'
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
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-9.7.1') { 
        // If you have configured more than one global server connection, you can specify its name
        bat "${scannerHome}/bin/sonar-scanner"
        bat "mvn sonar:sonar"
    }
        }
        }
       
    }
}
