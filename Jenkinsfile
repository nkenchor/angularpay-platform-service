// @Library('shared-pipeline-library') _
// deployGoApplication(
//     artifactId: 'platform-service',
//     serviceProfile: 'dev,elk',
//     doReinstall: 1,
//     binaryName: 'platform-service'
// )
pipeline {
    agent any
    tools {
            go 'go.1.17'
    }
    environment {
        GO117MODULE = 'on'
        APP_DIR = 'barafiri-platform-service'
		SERVICE_PROFILE = 'dev,elk'
		DO_REINSTALL = 1
		APP_TYPE= 'Service'
    }
    stages {
        stage('Build') {
            steps {
                       echo 'Compiling and building'
                       sh 'go build .'
                  }
        }
        stage('Deploy') {
            steps {
				sh 'sudo bash anaconda.directories ${APP_DIR} ${APP_TYPE}'
				sh 'sudo bash anaconda.ftp ${APP_DIR} ${APP_TYPE}'
				sh 'sudo bash anaconda.systemd ${APP_DIR} ${DO_REINSTALL}'
            }
        }
    }
}
