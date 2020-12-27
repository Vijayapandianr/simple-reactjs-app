import java.time.*
pipeline {
   agent any

   stages {
	   
    stage('Build'){
		steps{
		echo "Current workspace is ${env.WORKSPACE}"
		//sh '/usr/bin/zip lambda_function.zip lambda_function.py'
		}
    }

    stage('Push'){
		steps{
echo 'Push to S3 stage'
        //sh 'aws s3 cp lambda_function.zip s3://g10x-scango-s3-kaliraj-devops'
		}
    }

    stage('Deploy'){
		steps{
echo 'Deploy to Lamda stage'
 //       sh 'aws lambda create-function --function-name g10x-lambda-kaliraj2 --runtime python3.8 --code S3Bucket=g10x-scango-s3-kaliraj-devops,S3Key=lambda_function.zip --handler lambda_function.lambda_handler --region eu-west-1 --role arn:aws:iam::230315051295:role/service-role/g10x-lambda-kaliraj1-role-97cvwvru'
				}
    }
 }
}