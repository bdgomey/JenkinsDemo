pipeline {
    agent any

    stages{
        stage('Build Frontend'){
            steps{
                sh "echo Building frontend"
                sh "cd frontend"
                sh "npm install"
                sh "npm run build"
            }
        }
    }
}