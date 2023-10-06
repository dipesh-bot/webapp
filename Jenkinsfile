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
/*
stage ('Source-Code-Analysis') {
 steps {
	sh 'rm owasp* || true'
        sh 'wget "https://raw.githubusercontent.com/devopssecure/webapp/master/owasp-dependency-check.sh" '
	sh 'chmod +x owasp-dependency-check.sh'
	sh 'bash owasp-dependency-check.sh'
}
}
*/ 
stage ('SAST') {
	steps {
	withSonarQubeEnv('devsecops') {
		sh 'mvn sonar:sonar'
		sh 'cat target/sonar/report-task.txt'
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
}
