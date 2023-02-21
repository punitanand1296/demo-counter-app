pipeline {
    agent any
    stages{
        stage("git checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/punitanand1296/demo-counter-app.git'
            }
        }
    }
}