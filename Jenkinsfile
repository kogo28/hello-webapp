pipeline {
  agent { label 'jenkins-node' }

  triggers {
    pollSCM '* * * * *'
  }

  parameters {
    string defaultValue: '3.34.5.73', name: 'TOMCAT_IP'
    string defaultValue: 'ubuntu', name: 'TOMCAT_LOGIN_USER'
    string defaultValue: '/var/lib/tomcat9/webapps', name: 'TOMCAT_WEBAPP_DIR'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/c1t1d0s7/hello-webapp.git'
      }
    }

    stage('Maven Build') {
      tools { maven 'Maven-3' }
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        sh "scp ${env.WORKSPACE}/target/*.war ${params.TOMCAT_LOGIN_USER}@${params.TOMCAT_IP}:${params.TOMCAT_WEBAPP_DIR}"
      }
    }
  }
}
