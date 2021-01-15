pipeline {
    agent any /* {
         label 'sam_node'
    }*/

    stages {
        
        stage ('Checkout') {
            steps {
                checkout scm
                }
            }
        stage('Build') { 
            steps {
                bat 'npm install' 
            }
        }   
        
        stage('Start the App') { 
            steps {
                bat 'npm start' 
            }
        }   
        stage ('Deployment Build'){
            steps {
               bat 'npm run build'
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
