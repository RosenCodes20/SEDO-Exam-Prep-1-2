pipeline {
    agent any

    stages {
        stage('Prepare') {
            when {
                expression {
                    def allowed = ['main', 'hotfix/urgent-bug', 'feature/multiply-button', 'bugfix/subtract-empty']
                    return allowed.contains(env.BRANCH_NAME)
                }
            }
            steps {
                checkout scm
                echo "Building and testing branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Build') {
            when {
                expression {
                    def allowed = ['main', 'hotfix/urgent-bug', 'feature/multiply-button', 'bugfix/subtract-empty']
                    return allowed.contains(env.BRANCH_NAME)
                }
            }
            steps {
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Test') {
            when {
                expression {
                    def allowed = ['main', 'hotfix/urgent-bug', 'feature/multiply-button', 'bugfix/subtract-empty']
                    return allowed.contains(env.BRANCH_NAME)
                }
            }
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }

    post {
        always {
            echo "Finished pipeline for branch: ${env.BRANCH_NAME}"
            cleanWs()
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
