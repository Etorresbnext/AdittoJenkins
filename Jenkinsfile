pipeline{

    agent {label 'DES-BNEXT-152-etorres'}

    environment{
        ipAddressesList = ''
        pingResult = ''
        pingResultsList = ''
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
                        def pingOutput = powershell(script: "ping -n 1 ${ip}", returnStdout: true).trim()

                        if(pingOutput.contains("TTL=")){
                            pingResult = true
                        }
                        else{
                            pingResult = false
                        }
                        pingResultsList = pingResult.split("\n")
                    }
                    echo "${pingResultsList}"
                }
            }
        }
        stage('Post'){
            steps{
                script{
                    echo 'Hola Mundo'
                }
            }
        }
    }
}