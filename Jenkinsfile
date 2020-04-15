pipeline {
  environment {
    registry = "rajudevops05/canada-docker-webapp"
    registryCredential = 'dockerid'
    dockerImage = ''
  }
  agent any
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
    stage('Test') {
      steps {
        sh 'npm test'
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
   
  }
}