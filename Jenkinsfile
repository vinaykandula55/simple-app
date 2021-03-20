pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{

                    
                    nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'simple-app.1.0.0.war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '13.52.81.222:8081/repository/maven-releases/', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://13.52.81.222:8081/repository/maven-releases/', version: '1.0.0'
            }
        }
    }
}
