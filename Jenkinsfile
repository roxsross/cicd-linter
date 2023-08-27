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
                        env.REPO_NAME = env.GIT_URL.replace('.git', '').split('/').last()
                        echo $REPO_NAME
                        '''
                    }
                }
            }
        }
    }
}