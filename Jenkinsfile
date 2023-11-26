node {
  
  stage('SCM') {
    checkout scm
  }

  stage('SonarQube Analysis') {
    def mvn = tool 'mvn';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=tpCredicoop -Dsonar.projectName='tpCredicoop'"
    }
  }
  
  stage('Pusheo la nueva imagen a dockerhub y despliego con minikube') {
    sshagent(['claveSSH']) {
      sh 'ssh mvidaurre@192.168.19.135 "cd /home/mvidaurre/librosApp/dds-deploy && git pull && docker build -t mvidaurre08/dds-deploy:latest . && docker push mvidaurre08/dds-deploy:latest && kubectl apply -f postgres-deploy.yml && kubectl apply -f librosapp-deploy.yml"'
    }
  }
  
}

