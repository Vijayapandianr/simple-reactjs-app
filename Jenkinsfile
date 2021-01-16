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
                sh 'npm install' 
            }
        }   
        
        stage('Start the App') { 
            steps {
                sh 'npm run build' 
            }
        }   
        stage ('Deployment Build'){
            steps {
               sh 'npm start'
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
