pipeline {
    agent any
        environment {
            REPO_NAME= sh(script: "git remote show -n origin | grep Fetch | sed -r 's,.*:(.*).git,\\1,' |tr -d '\n'", returnStdout: true).trim()
        }
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
                        export $REPO_NAME
                        docker run --rm -v $(pwd):/dir stackrox/kube-linter lint --format json /dir/$REPO_NAME > kube-linter.json
                        '''
                    }
                }
            }
        }
    }
}