pipeline {
    agent any
    stages{
        stage("git checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/punitanand1296/demo-counter-app.git'
            }
        }
        stage("unit testing"){
            steps{
                sh 'mvn test'
            }
        }
        stage("integration testing"){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage("Maven Build"){
            steps{
                sh 'mvn clean install'
            }
        }
        stage("static code analysis"){
            steps{
                script{
                withSonarQubeEnv(credentialsId: 'jenkins-integration'){
                sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("quality gate status"){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-integration'
                }
            }
        }
        stage("war file upload"){
            steps{
                script{
                    nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], 
                    credentialsId: 'nexus-auth', 
                    groupId: 'com.example', 
                    nexusUrl: '54.196.190.74:8081', 
                    nexusVersion: 'nexus2', 
                    protocol: 'http', 
                    repository: 'demoapp-release', 
                    version: '1.0.0'
                }
            }
        }
    }
}