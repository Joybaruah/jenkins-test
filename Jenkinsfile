def remote = [:]
remote.name = 'rpi'
remote.host = '3.111.92.12'
remote.user = 'jenkins'
remote.port = 11702
remote.allowAnyHosts = true

pipeline {
    agent any
    triggers {
        githubPush()
    }
    environment {
        RPI_CREDS=credentials("ssh-agent-rpi")
    }
    stages {
        stage('Remote SSH') {
            steps {
                script {
                    remote.password=env.RPI_CREDS_PSW
                }
                sshCommand remote: remote, command: "cd /home/master/.node-red && df -h"
                // sshCommand remote: remote, command: "cd /home/master/.node-red && ./node-red-deployment.sh"
            }
        }
    }
}

