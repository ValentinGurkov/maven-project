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
                      bat "scp -v -i C:/Uasdasdasdasdsers/GreeN/Desktop/tomcat.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                  }
              }

              stage ("Deploy to Production"){
                  steps {
                      bat "scp -v -i C:/Useasdasdsadasdasrs/GreeN/Desktop/tomcat.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                  }
              }
          }
      }
  }
}