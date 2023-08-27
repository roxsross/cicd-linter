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
                        export REPO_NAME=${$GIT_URL/\.git/''}
                        echo $REPO_NAME
                        '''
                    }
                }
            }
        }
    }
}