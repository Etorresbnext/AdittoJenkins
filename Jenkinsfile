pipeline {
    agent {label 'DES-BNEXT-152-etorres'}
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Etorresbnext/AdittoJenkins.git', credentialsId: 'GitAditto'
            }
        }
        stage('Build') {
            steps {
                echo 'Hola Mundo'
            }
        }
    }
}

