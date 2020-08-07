pipeline { 
  agent any
  stages{
    stage('Build') {
      steps{
        echo "Building project"
      }
    }
     stage('Archive') {
      steps{
        echo "Archiving project"
      }
    }
     stage('Build docker image') {
      steps{
        echo "Building docker image"
      }
    }
     stage('push docker image') {
      steps{
        echo "pushing docker image"
      }
    }
     stage('Deploy to dev') {
      steps{
        echo "deploying to dev environment"
      }
    }
  }

}
