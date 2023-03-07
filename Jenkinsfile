pipeline {
  agent { label 'jenkins-node' }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/c1t1d0s7/hello-webapp.git'
      }
    }

    stage('Maven Build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        sh 'scp /var/lib/jenkins/workspace/maven_pipeline/target/hello-world.war ubuntu@172.31.42.138:/var/lib/tomcat9/webapps'
      }
    }
  }
}
