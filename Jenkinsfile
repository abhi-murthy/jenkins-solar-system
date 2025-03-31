pipeline {
    agent any

    tools {
        nodejs 'nodejs-23-10-0'
    }

    stages {
        stage ('Installing Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }
        stage ('NPM Dependencies Audit') {
            steps {
                sh '''
                    npm audit --audit-level=critical
                    echo $?
                '''
            }
        }
    }
}
