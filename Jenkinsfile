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
                    def ipAddressesList = getIpAddresses.split("\n")
                    echo "Lista de IPs: ${ipAddressesList}"
                }
            }
        }
        stage('Ping'){
            steps{
                script{
                    for (ip in ipAddressesList){
                        echo "Haciendo ping a: ${ip}"
                        powershell "ping -n 1 ${ip}"
                    }
                }
            }
        }
    }
}