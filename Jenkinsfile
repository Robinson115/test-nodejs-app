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
        MY_GIT_COMMIT = "${GIT_COMMIT}"
    }
    stages {
        stage('build') {
            steps {
                echo "Hello World!"
            }
        }
    }
    post{
        always{
            script{
                BUILD_USER = getBuildUser()
            }
            slackSend channel: '#test-slack',
                      color: COLOR_MAP[currentBuild.currentResult],
                      message: "*${currentBuild.currentResult}:* ${env.JOB_NAME} build ${env.BUILD_NUMBER} ${env.GIT_COMMIT} by ${BUILD_USER} \n More information at: ${env.BUILD_URL}"
        }
    }
}
