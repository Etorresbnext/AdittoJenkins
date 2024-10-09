pipeline{

    agent {label 'DES-BNEXT-152-etorres'}

    environment{
        ipAddressesList = ''
        connected = ''
    }

    stages{
        stage('Get'){
            steps{
                script{
                    def getIpAddresses = powershell(script: 'python C:\\Users\\etorres\\PycharmProjects\\IpAddresses\\main.py', returnStdout: true).trim()
                    ipAddressesList = getIpAddresses.split()
                }
            }
        }
        stage('Ping'){
            steps{
                script{
                    def pingResultsList = []
                    for(ip in ipAddressesList){
                        def getPingResult = powershell(script: "ping -n 1 ${ip}", returnStdout: true).trim()

                        if(getPingResult.contains("TTL=")){
                            isRunnerConnected = true
                        }
                        else{
                            isRunnerConnected = false
                        }
                        pingResultsList.add(isRunnerConnected)
                    }
                    connected = pingResultsList
                    echo "${connected}"
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