pipeline {
  environment {
    registry = "rajudevops05/canada-docker-webapp"
    registryCredential = 'dockerid'
    dockerImage = ''
  }
  agent any
  triggers {
        pollSCM('* * * * *')
    }
 tools {nodejs "nodejs" }
  stages {
    stage('Cloning Git') {
      steps {
        git url: 'https://github.com/raju-ranjan/docker-demo.git'
      }
    }

    stage('Build') {
       steps {
         sh 'npm install'
       }
    }
   
    
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
	 stage('Run Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            sh 'docker run -i -p 3000:3000 rajudevops05/canada-docker-webapp:$BUILD_NUMBER'
          }
        }
      }
    }
   
  }
}
