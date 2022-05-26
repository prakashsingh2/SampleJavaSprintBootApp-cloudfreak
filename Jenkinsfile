pipeline {
  agent any
    tools {
      maven 'rakhimaven'
                 jdk 'rakhijdk'
    }
    stages {      
        stage('Build maven ') {
            steps { 
                    sh 'pwd'      
                    sh 'mvn  clean install package'
            }
        }
        
        stage('Copy Artifact') {
           steps { 
                   sh 'pwd'
		   sh 'cp -r target/*.jar docker'
           }
        }
         
        stage('Build docker image') {
           steps {
               script {         
                 def customImage = docker.build('application/rakhi', "./docker")
                 docker.withRegistry('https://rakhiregistry.azurecr.io', 'rakhiacr') {
                 customImage.push("${env.BUILD_NUMBER}")
                 }                     
           }
        }
	  }
    }
}
