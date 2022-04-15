pipeline {
  agent any
  tools {
    maven 'M2_HOME'
  }
  environment { 
    registry = "mjjohnson94/devops-pipeline" 
    registryCredential = 'DockerID'
  }
  stages {
    stage('build'){
      steps {
      sh 'mvn clean'
      sh 'mvn install'
      sh 'mvn package'  
      }
    }
    stage('test'){
      steps {
      echo "test step"
      sh 'mvn test'
      }
    }
    stage('deploy'){
      steps {
       script {
        docker.build registry + ":$BUILD_NUMBER"
        }
      }
       stage('Deploy Image') {
        steps{
         script {
          docker.withRegistry( 'DockerID', registryCredential ) {
           dockerImage.push()
          } 
        }
      }
    }
  }
}
