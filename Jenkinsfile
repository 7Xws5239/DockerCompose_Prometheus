pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                script {
                    def currentDir = sh(script: 'pwd', returnStdout: true).trim()
                    echo "Current directory is: ${currentDir}"

                    sshCommand remote: [
                        name: 'remote-server',
                        host: '124.71.189.214',
                        user: 'root',
                        identityFile: "${currentDir}/huawei_bowman.pem", // 使用获取到的工作目录路径
                        port: 22,
                        allowAnyHosts: true
                    ], command: '''
                        echo Hello from remote server;
                        ls -l;
                        uptime
                    '''
                }
            }
        }
    }
}
