pipeline { 
  environment {
    registry = "docker3032/petclinic"
    registryCredential = "docker_hub_docker3032"
    dockerImage = ""
  }
  agent any
  stages{
    stage('Build') {
      steps{
        echo "Building project"
         sh './mvnw package'
      }
    }
     stage('Archive') {
      steps{
        echo "Archiving project"
        archiveArtifacts artifacts: '**/*.jar', followSymlinks: false
      }
    }
     stage('Build docker image') {
      steps{
        echo "Building docker image"
        script{
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
     stage('push docker image') {
      steps{
        echo "pushing docker image"
        script{
          docker.withRegistry( "", registryCredential){
          dockerImage.push()
         

          }
        }
      }
    }
     stage('Deploy to dev') {
      steps{
        echo "deploying to dev environment"
      }
    }
  }

}
