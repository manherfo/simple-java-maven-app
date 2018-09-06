pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
             steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'ls ; ./jenkins/scripts/deliver.sh'
            }
        }
        stage('email'){
            steps{
                emailext body: 'hola', recipientProviders: [developers()], subject: 'hola', to: 'mao.11.hf@gmail.com
            }
        }
    }
}
