pipeline {
  agent any
  tools {
    maven 'Maven'
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
	  
stage ('SAST') {
	steps {
	withSonarQubeEnv('sonar') {
		sh 'mvn sonar:sonar'
		sh 'cat target/sonar/report-task.txt'
	}
	} 
}

stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

 stage ('Deploy-To-Tomcat') {
      steps {
        sshagent(['tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.80.84.187:/prod/apache-tomcat-8.5.94/webapps/webapp.war'
        }
      }
}   
}
}

