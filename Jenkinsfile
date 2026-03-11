node {
    checkout scm

    stage("Build") {
        docker.image('composer:2.7').inside('-u root') {
            sh '''
            git config --global --add safe.directory /var/jenkins_home/workspace/Laraveldev
            composer install --no-interaction --prefer-dist
            '''
        }
    }

    stage("Test") {
        docker.image('ubuntu:22.04').inside('-u root') {
            sh 'echo "Ini adalah test stage Jenkins pipeline"'
        }
    }
}
