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
		
		sh 'ant -f test.xml -v'
		
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-9.jar jenkins-s3bucket-deok93jvvow.s3.amazonaws.com'

	}   
	
	stage('Results') { 
   
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'b3a6dfa3-d823-44cd-b040-d6f026c752cf', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {    
			sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'    		}
			
	}

}
