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
                    def repName = checkout(scm).repoName
                    sh "echo 'Repository Name is: ${repName}'"
                    println repName
                    steps {
                        sh '''
                        echo "hola"
                        '''
                    }
                }
            }
        }
    }
}