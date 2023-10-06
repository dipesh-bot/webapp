pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages {
    stage('Initialize') {
      steps {
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
stage ('Check-git-Secrets') {
	steps {
       sh 'rm trufflehog || true'
      sh 'docker run -t gesellix/trufflehog --json https://github.com/dipesh-bot/webapp.git > trufflehog'
      sh 'cat trufflehog'
}
}
stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    /*
    stage ('Deploy-To-Tomcat') {
      steps {
        sshagent(['192.168.182.130']) {
          sh 'scp -o StrictHostKeyChecking=no target/*.war dipesh1@192.168.182.131:/prod/apache-tomcat-8.5.93/webapps/webapp.war'
        }
      }
} */    
  }
}

