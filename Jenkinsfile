node {

    env.PROD_HOST = "prod.kelasdevops.xyz"

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

    stage("Deploy Prod") {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {

            sshagent (credentials: ['ssh-prod']) {

                sh "mkdir -p ~/.ssh"
                sh "ssh-keyscan -H ${PROD_HOST} >> ~/.ssh/known_hosts"

                sh """
                rsync -rav --delete ./ \
                ubuntu@${PROD_HOST}:/home/ubuntu/prod.kelasdevops.xyz/ \
                --exclude=.env \
                --exclude=storage \
                --exclude=.git
                """
            }
        }
    }
}
