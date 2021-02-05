 pipeline {
    agent any /* {
         label 'sam_node'
    }*/
    
     tools { nodejs "nodejs" }

    stages {
        
        stage ('Checkout') {
            steps {
	cleanWs()
                checkout scm
                }
            }
	
        stage('Install') { 
            steps {
                sh 'npm install' 
            }
        }
        
        stage('Build') { 
            steps {
                sh 'npm run build' 
            }
        }   
        stage ('Zipping'){
            steps {
               sh '/usr/bin/zip -r build-$BUILD_NUMBER.zip . -i build/*'
            }
        }
        stage ('Copy to S3'){
            steps {
               sh 'aws s3 cp build-$BUILD_NUMBER.zip s3://mystorage-s3/react/'
            }
        }
        stage ('Deploy to Lambda'){
            steps {
               sh 'aws lambda update-function-code  --function-name react-app-function  --region ap-south-1  --s3-bucket mystorage-s3 --s3-key react/build-$BUILD_NUMBER.zip'
            }
        }
        
        
    }
    
    post {
        always {
            emailext attachLog: true, 
	                                  
	                                  body: """Build ${currentBuild.currentResult}: Job ${env.JOB_NAME} (Build Number# [${env.BUILD_NUMBER}])</br>
                                     Check console output at :${env.BUILD_URL}  > ${env.JOB_NAME} [${env.BUILD_NUMBER}]""",
	                                  to: 'vijayganesh6@gmail.com',
	                                  subject: "Build ${currentBuild.currentResult}: Job ${env.JOB_NAME} (Build Number# [${env.BUILD_NUMBER}])"
        }
        
    }
}
