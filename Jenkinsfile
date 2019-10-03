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
              bat 'mvn clean package'
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
              bat "echo y|pscp -i \"C:\path\my-key-pair.ppk\" \"C:\path\Sample_file.txt\" ec2-user@public_dns:/home/ec2-user/Sample_file.txt"
              
              
              
              
              //ec2-user@18.223.22.16:/var/lib/tomcat7/webapps"
          }
      }
  }
}
