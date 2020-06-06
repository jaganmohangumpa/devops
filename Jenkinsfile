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
    
  }
}
