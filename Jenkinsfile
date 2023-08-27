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
                stage("Linter Kubelinter") {
                    agent {
                        docker {
                            image "stackrox/kube-linter"
                            args "--volume ${WORKSPACE}:/dir"
                            reuseNode true
                        }
                    }
                    steps {
                        script {
                            def result = sh label: "Kube-linter", returnStatus: true,
                                script: """\
                                    kube-linter lint --format json /dir/$GITHUB_REPO_NAME
                            """
                            if (result > 0) {
                                unstable(message: "Kube-linter issues found")
                            }   
                        }
                    }
                }
            }
        }
    }
}