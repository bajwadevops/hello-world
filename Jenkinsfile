pipeline {
  agent any
  environment {
   
    dockerHubRepo='bajwadocker'
    dockerImageName = 'hello-world'
	
	}  
   stages {
   stage('Build Image') {
      steps {
        sh "docker build -t ${dockerHubRepo}/${dockerImageName}:v2 ."
      }
    }
    stage('Deploy Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerhub_Pass', usernameVariable: 'dockerhub_User')]) {
          sh 'docker login -u "${dockerhub_User}" -p "${dockerhub_Pass}" '
          sh 'docker push "${dockerHubRepo}"/"${dockerImageName}":v2'
        }
      }	
    }
  
}
