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
            withCredentials([sshUserPrivateKey(credentialsId: "mykeyid", keyFileVariable: 'keyfile')]) {
        sh "scp -i ${keyfile} dist/trainSchedule.zip centos@3.20.126.40:/tmp"
        }
      }
    }
  }
}
