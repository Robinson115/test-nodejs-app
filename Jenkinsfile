def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger'
]

def getBuildUser(){
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

pipeline {
    agent any
    
    environment{
        BUILD_USER=''
    }
    stages {
        stage('build') {
            steps {
                echo "Hello World!"
            }
        }
    }
    post {
        unstable {
            slackSend channel: "#ci-builds", color: COLOR_MAP[currentBuild.currenResult], message: "${env.BUILD_TAG} success with change :\n" +
                "commit ${env.CHANGE_ID}\n" +
                "Author: ${env.CHANGE_AUTHOR_DISPLAY_NAME} <${env.CHANGE_AUTHOR_EMAIL}>\n" +
                "\t${env.CHANGE_TITLE}\n" +
                "See : ${env.JOB_URL}"
    }
        failure {
           slackSend channel: "#ci-builds", color: COLOR_MAP[currentBuild.currenResult], message: "${env.BUILD_TAG} failed with change :\n" +
               "commit ${env.CHANGE_ID}\n" +
               "Author: ${env.CHANGE_AUTHOR_DISPLAY_NAME} <${env.CHANGE_AUTHOR_EMAIL}>\n" +
               "\t${env.CHANGE_TITLE}\n" +
               "See : ${env.JOB_URL}"
}
