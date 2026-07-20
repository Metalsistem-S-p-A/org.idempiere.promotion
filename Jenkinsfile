pipeline {
    agent {
        label 'master'
    }

    options {
        timestamps()
    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean verify -Drepos.idempiere=/var/lib/jenkins/workspace/idempiere'
            }
        }
    }
}
