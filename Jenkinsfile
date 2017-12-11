properties([pipelineTriggers([githubPush()])])



node('linux') {   
	
	stage('Test') {    
		
		git 'https://github.com/tsongfwmoua/java-project.git'
		
		sh 'ant -f test.xml -v'

		junit 'reports/result.xml' 
	
	}   
	
	stage('Build') {    
		
		sh 'ant -f build.xml -v'
	
	} 
	
	stage('Deploy') {    
		
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://jenkins-s3bucket-1l824w8p6lw7d/'

	}   
	
	stage('Results') { 
   
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'cfaeeaf2-f714-4570-a0e5-d2e1df2de00f', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {    
			sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'    		}
			
	}

}
