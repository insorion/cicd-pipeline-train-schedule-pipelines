pipeline {
  agent any
  stages {
    stage ('build'){
      steps {
        echo "Running build automation"
        sh "gradle wrapper --gradle-version=5.1.1 build --no-daemon"
        archiveArtifacts artifacts: "dist/trainSchedule.zip"
      }
    }
  }
}
