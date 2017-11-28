properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/tsongfwmoua/java-project.git'
		sh ‘ant -f build.xml -v’  
	}   
	stage('Build') {    
		sh 'ant -f test.xml -v'
	}   
	stage('Results') {    
		junit 'reports/*.xml'   
	}
}
