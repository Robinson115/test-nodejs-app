pipeline {
    agent
    stages {
        stage('build') {
            steps {
                echo "Hello World!"
            }
        }
    }
    post {
        success {
            sh 'printenv'
            emailext body: '$PROJECT_DEFAULT_CONTENT Commit message: ${FILE, path="commit_message.txt"}\nThis commit: ${GIT_COMMIT}Build URL: ${BUILD_URL}',
            recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'CulpritsRecipientProvider'], [$class: 'RequesterRecipientProvider']],
            subject: 'Some subject'
        }
    }
}
