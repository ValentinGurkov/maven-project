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
          }
          post {
              success {
                  echo 'Now Archiving...'
                  archiveArtifacts artifacts: '**/target/*.war'
              }
          }
      }

      stage ('Deployments'){
          parallel{
              stage ('Deploy to Staging'){
                  steps {
                     bat "scp -v -i  /tomcat.pem **/target/*.warp.war ec2-user@18.217.255.114:/var/lib/tomcat8/webapps"
                  }
              }

              stage ("Deploy to Production"){
                  steps {
                      bat "ls -la"
                     bat "scp -v -i  tomcat.pem **/target/*.warp.war ec2-user@52.14.139.125:/var/lib/tomcat8/webapps"
                  }
              }
          }
      }
  }
}
