node{
    def mavenHome = tool name : "maven3.6.3"
	stage('CheckoutCode')
	{
		git branch: 'development', credentialsId: '75bc12f9-791b-49a4-9443-d2227911f3ff', url: 'https://github.com/yaminireddy05/maven-web-application.git'
	}
	stage('Build')
	{
		sh "${mavenHome}/bin/mvn clean package"
	}
	stage('ExecuteSonarQubeReport')
	{
		sh "${mavenHome}/bin/mvn sonar:sonar"
	}
	stage('UploadArtifactoryIntoNexus')
	{
		sh "${mavenHome}/bin/mvn deploy"
	}
	stage('DeployAppIntoTomcatServer')
	{
	sshagent(['6236a586-3dd1-4efb-8362-8d787d392e2c']) {
    sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war ec2-user@52.66.236.78:/opt/apache-tomcat-9.0.41/webapps/"
    }
	}
	stage('SendEmailNotification')
	{
	mail bcc: '', body: '''Build over



	Regards
	K.yamini
	87886798900 ''', cc: 'kyamini221@gmail.com', from: '', replyTo: '', subject: 'Build over ', to: 'kyamini221@gmail.com'
	}

}
