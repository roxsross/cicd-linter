pipeline {
    agent any
    stages {
        stage('Check Linters') {
            parallel {
                stage('Linter Hadolint') {
                    steps {
                        sh 'docker run --rm -i hadolint/hadolint < Dockerfile'      
                    }

                }
                stage('Linter Kube-linter') {
                    steps {
                        sh '''
                        echo $GIT_URL
                        echo REPO_NAME=$($GIT_URL.tokenize('/.')[-2])
                        echo $REPO_NAME
                        '''
                    }
                }
            }
        }
    }
}