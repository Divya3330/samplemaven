pipeline {
   agent any
    environment {
  
        registryCredential = 'dockerhub_id'
        registry = "divya333/samplemaven"
        dockerImage = ''
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Divya3330/samplemaven.git']]])  
            }
        }
    stage('Build') {
		  steps {
			  sh "echo Packaging Sample MiddleWare Application"
			  sh "mvn clean package"
		  }
    }
  
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }
    stage('Upload Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
 
    }
}
