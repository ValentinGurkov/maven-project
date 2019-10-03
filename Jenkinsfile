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

// tools {
//   maven 'localMaven'
//   jdk 'localJDK'
// }
//
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
            sh "scp -o StrickHostKeyChecking=no -i /home/green/ssh/tomcat.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
              //bat "scp -v -i  /c:/tomcat.ppk **/target/*.warp.war ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"

              //bat "ls -la"
              //bat "echo y|pscp -i \"C:\\tomcat.ppk\" \"webapp\\target\\*.war\" ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"
          }
      }
  }
}
