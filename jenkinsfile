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
									      artifactId: 'samplesnap',
										  classifier: '',
										  file: "/var/lib/jenkins/workspace/sampletest/target/samplesnap-${mavenPom.version}.war",
										  type: 'war'
								    ]
							], 
				      			credentialsId: '7838',
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
