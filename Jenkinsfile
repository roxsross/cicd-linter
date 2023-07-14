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
                        export REPO_NAME=${git_url/\.git/''}
                        docker run --rm -v $(pwd):/dir stackrox/kube-linter lint --format json /dir/$REPO_NAME > kube-linter.json
                        '''
                    }
                }
            }
        }
    }
}