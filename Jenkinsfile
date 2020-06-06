pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo Building...'
        sh '''
          echo "Multiline shell step works too"
          ls -lah
        '''
      }
    }
    stage('lint') {
      steps {
        sh 'tidy -q -e ./app/index.html'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t jaganmohangumpa/devops .'
      }
    }
    stage('Push Docker Image') {
      steps {
        withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
          sh 'docker push jaganmohangumpa/devops'
        }
      }
    }
    stage('Deployment') {
      steps {
        sh 'echo eks...'
        sh '''
          echo "eks shell step works too"
          aws eks --region us-east-1 update-kubeconfig --name capstone-ekscluster
          kubectl apply -f blue-deployment.json 
          kubectl apply -f green-deployment.json
          kubectl apply -f app-service.json
        '''
      }
    }
    stage('Clean Up') {
      steps {
        sh 'docker system prune'
      }
    }
  }
}
