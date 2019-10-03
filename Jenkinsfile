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
    string(name:'tomcat_dev', defaultValue:'18.223.22.16', description: 'Staging Server')
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
            bat "ls /c:/"
            //sh "scp -o StrictHostKeyChecking=no -i /home/green/ssh/tomcat.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
            bat "scp -o StrictHostKeyChecking=no -i /c:/tomcat.pem **/target/*.warp.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
          }
      }
  }
}
