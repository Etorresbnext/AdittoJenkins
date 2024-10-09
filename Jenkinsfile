pipeline{

    agent {label 'DES-BNEXT-152-etorres'}

    environment{
        ipAddressesList = ''
        runnersConnectionList = ''
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
                    runnersConnectionList = pingResultsList
                }
            }
        }
        stage('Post'){
            steps{
                script{
                    for(int i = 0; i < ipAddressesList.size(); i++){
                        def ip = ipAddressesList[i]
                        echo "${ip}"
                        def connected = runnersConnectionList[i]
                        echo "${connected}"

                        powershell "python C:\\Users\\etorres\\PycharmProjects\\IpAddresses\\update_runners_connection.py ${connected} ${ip}"
                    }
                }
            }
        }
    }
}