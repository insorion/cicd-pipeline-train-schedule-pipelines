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
            withCredentials([sshUserPrivateKey(credentialsId: "mykeyid", keyFileVariable: 'keyfile')]) {
       stage('deployToStagind') {
        sh "scp -i ${keyfile} dist/trainSchedule.zip ec2-user@3.20.126.40:/tmp"
      }
    }
  }
}
