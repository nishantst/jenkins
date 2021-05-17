pipeline {
      agent any
	  tools {
	        maven 'maven-3'
			
	  }
      stages{
             stage('Build'){
                     steps{
                              sh script: 'mvn clean package'
                      }

                } 
             stage('Upload war to nexus'){
                     steps{
						 script{
                              def mavenPom = readMavenPom file: 'pom.xml'
                              nexusArtifactUploader artifacts: [
							         [
									      artifactId: 'maven-deploy-plugin',
										  classifier: '',
										  file: "/var/lib/jenkins/workspace/nexus/target/maven-deploy-plugin-${mavenPom.version}.war",
										  type: 'war'
								    ]
							], 
				      			credentialsId: 'be80dbe5-7e11-4687-8290-ce503998e63f',
				      			groupId: 'com.jdevs',
				      			nexusUrl: '13.89.109.174::8081',
				      			nexusVersion: 'nexus3',
				      			protocol: 'http',
				      			repository: 'maven-snapshots',
				      			version: "${mavenPom.version}"
						 }
							}
                    }
         }
}		 
