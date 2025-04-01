pipeline {
    agent {
        any
        retries 2
    }
    tools {
        nodejs 'nodejs-23-10-0'
    }

    stages {
        stage ('Installing Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }
        stage ('Dependency scanning') {
            parallel {
                stage ('NPM Dependencies Audit') {
                    steps {
                        sh '''
                            npm audit --audit-level=critical
                            echo $?
                        '''
                    }
                }
                stage('OWASP Dependency Check') {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan \'./\' 
                            --out \'./\'  
                            --format \'ALL\' 
                            --prettyPrint''', odcInstallation: 'OWASP-DepCheck-12'
                    }
                }
            }
        }
    }
}
