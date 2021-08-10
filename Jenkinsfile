pipeline {

  agent any

  stages {


    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }
  
   stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "webdeploy.yml")
        }
      }
    }

  }

}
