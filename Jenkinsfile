pipeline {
    agent any

    stages{
        stage('Build Frontend'){
            steps{
                sh "echo Building frontend"
                sh "cd frontend && npm install && npm run build"
                
            }
        
            }
        stage('Deploy Frontend'){
            steps{
                script{
                  withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                   sh "aws s3 sync frontend/dist s3://bjgomes-bucket-sdet" 
                    }  
                }
            }
        }
        stage('Build Backend'){
            steps{
                sh "cd demo && mvn clean install"
            }
        }
    }
}