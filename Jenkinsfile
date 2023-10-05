pipeline {
  agent any
  tools {
    // Use single quotes for tool names
    maven ""Maven""
  }
  stages {
    stage('Initialize') {
      steps {
        // Corrected the interpolation syntax
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    stage('Build') {
      steps {
        // Removed unnecessary single quotes
        sh 'mvn clean package'
      }
    }
  }
}

