pipeline {
  agent any
  stages {
    stage ('build'){
      steps {
        echo "Running build automation"
        sh "java -version"
        sh "./gradlew --info build --no-daemon"
        archiveArtifacts artifacts: "dist/trainSchedule.zip"
      }
    }
           stage('deployToStagind') {
             steps {
                   withCredentials([sshUserPrivateKey(credentialsId: 'priv_2', keyFileVariable: 'KEY')]) {
                     script {
                     echo ${KEY}
                     }
                     sh "ssh -i ${KEY} centos@3.20.126.40 -C \'hostname\'"
                   
        }
      }
    }
  }
}
