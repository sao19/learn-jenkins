pipeline {
  agent none 
  tools {
    maven 'Maven'
  }

  stages {
    stage('Build') {
      steps {
        script {
          echo "Building the application....."
          mvn package
          docker build -t localhost:8083/my-app:jenkins-pipeline
        }
      }
    }

    stage('Push to registry') {
      steps {
        script {
          echo "Push the application to registries......"
          withCredentials([usernamePasswod(credentialId: 'nexus', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
            echo "$PASS" | docker login -u "$USER" --pasword-stdin localhost:8083
            docker push localhost:8083/my-app:jenkins-pipeline
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
