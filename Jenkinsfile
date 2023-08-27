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
                        env.REPO_NAME = env.GIT_URL.replace('.git', '').split('/').last()
                        docker run --rm -v $(pwd):/dir stackrox/kube-linter lint --format json /dir/$REPO_NAME > kube-linter.json
                        '''
                    }
                }
            }
        }
    }
}