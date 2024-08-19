pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'll'
                sshCommand remote: [
                    name: 'remote-server',
                    host: '124.71.189.214',
                    user: 'root',
                    identityFile: 'huawei_bowman.pem',
                    port: 22,
                    allowAnyHosts: true
                ], command: 'echo Hello from remote server'
            }
        }
    }
}
