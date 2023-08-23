pipeline {
  agent any 
  tools {
    maven 'Maven'
  }

  stages {
    stage('Build Jar') {
      steps {
        script {
          echo "Building the application....."
          sh 'mvn package'
        }
      }
    }

    stage('Create Image') {
      steps {
        script {
          echo "Push the application to registries......"
          sh 'docker build -t localhost:8083/my-app:jenkins-pipeline'
          withCredentials([usernamePasswod(credentialId: 'nexus', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            sh "echo $PASS | docker login -u $USER --pasword-stdin localhost:8083"
            sh 'docker push localhost:8083/my-app:jenkins-pipeline'
          }
        }
      }
    }

    stage('Deploy') {
      steps {
        script {
          echo "Deploying the application........"
        }
      }
    }
  }
}
