node {
  
  stage('SCM') {
    checkout scm
  }

  stage('Build and Push Docker Image') {
    sshagent(['claveSSH']) {
      sh 'ssh mvidaurre@192.168.19.135 "cd $HOME/librosApp && git pull && docker build -t mvidaurre08/dds-deploy:ultima_version . && docker push mvidaurre08/dds-deploy:ultima_version"'
    }
  }
}
  
  stage('SonarQube Analysis') {
    def mvn = tool 'mvn';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=tpCredicoop -Dsonar.projectName='tpCredicoop'"
    }
  }

