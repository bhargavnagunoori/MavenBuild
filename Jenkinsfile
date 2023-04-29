node(){

	
	stage('Code Checkout'){
		checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCreds', url: 'https://github.com/bhargavnagunoori/MavenBuild']])
	}
	stage('Build Automation'){
		sh """
			ls -lart
			mvn clean install
			ls -lart target
		"""
	}
	

	stage('Code Deployment'){
		deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://44.211.70.34:8080/')], contextPath: 'bhargav', onFailure: false, war: 'target/*.war'
	}

	stage('email notification'){
		mail bcc: '', body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>""", cc: , from: '', replyTo: '', 
		subject: 'Test Application Notification', to: 'bargav414@gmail.com'
		
}
}
