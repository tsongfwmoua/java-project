pipeline {
	agent any
	stage(‘Build’) {
		sh ‘ant -f build.xml -v’
	}
	stage(‘Test’) {
		sh 'ant -f test.xml -v'
		junit ‘reports/*.xml’
	}
}
