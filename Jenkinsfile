//pipeline {
//  agent any
//
//  tools {
//    maven 'localMaven'
//    jdk 'localJDK'
//  }
//
//  triggers {
//    pollSCM('* * * * *')
//  }
//
//  stages {
//      stage('Build'){
//          steps {
//              bat 'mvn clean package'
//              bat "docker build . -t tomcatwebapp:${env.BUILD_ID}"
//          }
//
//      }
//  }
//}

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
              sh 'mvn clean package'
          }
          post {
              success {
                  echo 'Now Archiving...'
                  archiveArtifacts artifacts: '**/target/*.war'
              }
          }
      }

      stage ('Deploy to Staging'){
          steps {
            scp "scp -v -i  /home/ssh/tomcat.pem **/target/*.war ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"
              //bat "scp -v -i  /c:/tomcat.ppk **/target/*.warp.war ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"

              //bat "ls -la"
              //bat "echo y|pscp -i \"C:\\tomcat.ppk\" \"webapp\\target\\*.war\" ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"
          }
      }
  }
}
