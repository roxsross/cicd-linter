pipeline {
    agent any
        environment {
        GITHUB_REPO_NAME = env.GIT_URL.replaceFirst(/^.*\/([^\/]+?).git$/, '$1')
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
                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        sh '''
                        echo $GITHUB_REPO_NAME
                        docker run --rm -v $(pwd):/dir stackrox/kube-linter lint --format json /dir/$GITHUB_REPO_NAME > kube-linter.json
                        stash includes: 'kube-linter.json', name: 'kube-linter.json'
                        '''
                        }
                    }
                }
            }
        }
    }
}