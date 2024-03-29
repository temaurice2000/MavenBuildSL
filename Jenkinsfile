pipeline {
	agent {
		node {
			label 'Ubuntu'
		}
	}
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			bat "mvn clean install -Dmaven.test.skip=true"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	
	stage('deployment'){
		steps{
		//deploy adapters: [tomcat9(credentialsId: 'TomcatCreds' path: '', url: 'http://52.90.187.236:8080/')], contextPath: 'counterwebapp', war: 'target/*.war'
		deploy adapters: [tomcat9(url: 'http://10.10.10.121:8080/', 
                              credentialsId: 'TomcatCreds')], 
                     war: 'target/*.war',
                     contextPath: 'app'
		}
		
	}
	
	stage('Notification'){
		steps{
		emailext(
			subject: "Job Completed",
			body: "Jenkins pipeline job for maven build job completed",
			to: "temaurice2000@yahoo.fr"
		)
		}
	}
	}
}
