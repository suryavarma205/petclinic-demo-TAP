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
          dockerImage.push('latest')

          }
        }
      }
    }
     stage('Deploy to dev') {
      steps{
        echo "deploying to dev environment"
        sh "dockerrm -f petclinic || true"
        sh "docker run -d --name=petclinic -p 8081:8080 docker3032/petclinic"
      }
    }
  }

}
