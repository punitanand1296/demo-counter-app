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
    }
}