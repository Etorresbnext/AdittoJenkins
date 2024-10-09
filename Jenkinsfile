pipeline{

    agent {label 'DES-BNEXT-152-etorres'}

    environment{
        ipAddressesList = ''
    }

    stages{
        stage('Get'){
            steps{
                script{
                    def getIpAddresses = powershell(script: 'python C:\\Users\\etorres\\PycharmProjects\\IpAddresses\\main.py', returnStdout: true).trim()
                    ipAddressesList = getIpAddresses.split("\n")
                }
            }
        }
        stage('Ping'){
            steps{
                script{
                    for(ip in ipAddressesList){
                        def pingResult = powershell(script: "ping -n 1 ${ip}", returnStdout: true).trim()
                        echo "${pingResult}"
                    }
                }
            }
        }
    }
}