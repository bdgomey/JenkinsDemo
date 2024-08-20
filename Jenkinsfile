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
                    try {
                      withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                        sh "aws s3 sync frontend/dist s3://bjgomes-bucket-sdet" 
                        }
                    }catch (Exception e) {
                            echo "${e}"
                            throw e
                    }   
                }
            }
        }
        stage('Build Backend'){
            steps{
                sh "cd demo && mvn clean install && ls target/"
            }
        }
        stage('Test Backend'){
            steps{
                sh "cd demo && mvn test"
            }
        }
        stage('Deploy Backend'){
            steps{
                script{
                  withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                        sh 'pwd'
                        sh "aws s3 sync demo/target/*.jar s3://bjgomes-bucket-sdet-backend"
                        sh "echo 'aws elasticbeanstalk create-application-version --application-name myName --version-label 0.0.1 --source-bundle S3Bucket=\"bjgomes-bucket-sdet-backend\",S3Key=\"demo-1.0-SNAPSHOT.jar\"'"
                        sh "ech 'aws elasticbeanstalk update-environment --environment-name myName --version-label 0.0.1'"
                    }  
                }   
            }
        }
    }
}