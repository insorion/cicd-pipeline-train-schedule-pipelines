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
    stage ('DeployToStagind') {
        when {
            branch 'master'
        }
        steps {
            withcredetials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                failOnError="true",
                continueOnError: false,
                publishers: [
                    sshPublisherDesc(
                        configName: 'staging',
                        sshCredentials: [
                            username: "$USERNAME",
                            encryptedPassphrase: "$USERPASS"
                        ],
                        transfers: [
                            sshTransfer(
                                sourceFiles: 'dist/trainSchedule.zip',
                                removePrefix: 'dist/',
                                remoteDirectory: '/tmp',
                                
                            )
                        ]
                    )
                ]

            }

        }
    }
  }
}
