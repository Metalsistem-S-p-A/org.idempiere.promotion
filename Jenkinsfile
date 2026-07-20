pipeline {
    agent {
        label 'master'
    }

    environment {
        PLUGIN_NAME = 'org.idempiere.promotion'
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Check changes') {
            steps {
                script {
                    def changed = sh(
                        script: "git diff --name-only HEAD~1 HEAD -- ${PLUGIN_NAME} | wc -l",
                        returnStdout: true
                    ).trim()
                    if (changed == '0') {
                        currentBuild.result = 'NOT_BUILT'
                        error("Nessuna modifica in ${PLUGIN_NAME}, skip build")
                    }
                }
            }
        }

        stage('Build') {
            steps {
                dir(PLUGIN_NAME) {
                    sh 'mvn clean verify -Drepos.idempiere=/var/lib/jenkins/workspace/idempiere'
                }
            }
        }

    }
}
