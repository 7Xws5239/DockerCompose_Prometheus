pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                script {
                    def currentDir = sh(script: 'pwd', returnStdout: true).trim()
                    echo "Current directory is: ${currentDir}"
                    
                    sh """ 
                    chmod 600 ${currentDir}/huawei_bowman.pem
                    scp -i ${currentDir}/huawei_bowman.pem -o StrictHostKeyChecking=no ${currentDir}/docker-compose.yml root@124.71.189.214:/root/dockercompose    
                    """ //别用单引号，没法搞字符串插值，不解析的；另外别放进去，放进去直接识别为命令了
                    sshCommand remote: [
                        name: 'remote-server',
                        host: '124.71.189.214',
                        user: 'root',
                        identityFile: "${currentDir}/huawei_bowman.pem", // 使用获取到的工作目录路径
                        port: 22,
                        allowAnyHosts: true
                    ], command: '''
                        echo Hello from remote server;
                        tar xzvf /root/download/prom.tar.gz -C /root/download
                        cd /root/download/prom
                        docker-compose up
                    '''
                }
            }
        }
    }
}
