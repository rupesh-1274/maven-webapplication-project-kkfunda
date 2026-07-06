node
{

		// /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.9/bin
	def mavenHome =tool name: "maven-3.9.9"
	stage('Git checkout')
	{
		git branch: 'development', url: 'https://github.com/rupesh-1274/maven-webapplication-project-kkfunda.git'
	}
	stage('Maven Build')
	{
		sh " ${mavenHome}/bin/mvn clean package"
	}

	stage('Sonarqube')
	{
		sh " ${mavenHome}/bin/mvn sonar:sonar"
	}
	stage(' deploy into Nexus')
	{
		sh " ${mavenHome}/bin/mvn deploy"
	}
	stage('Deploy onto Tomcat')
	{
		sh """

      curl -u kk:password \
      --upload-file /var/lib/jenkins/workspace/jio-scriptedway-pipeline/target/maven-web-application.war \
      "http://3.0.17.234:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
	}
}
