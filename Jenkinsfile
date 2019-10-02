pipeline {
  agent any

  tools {
    maven 'localMaven'
    jdk 'localJDK'
  }

  parameters {
    string(name:'tomcat_dev', defaultValue:'18.217.255.114', description: 'Staging Server')
    string(name:'tomcat_prod', defaultValue:'52.14.139.125', description: 'Production Server')
  }

  triggers {
    pollSCM('* * * * *')
  }

  stages {
      stage('Build'){
          steps {
              bat 'mvn clean package'
              bat "docker build . -t tomcatwebapp:${env.BUILD_ID}"
          }

      }
  }
}
