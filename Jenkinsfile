pipeline {
    agent any
    stages {
        stage('compile') {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage('test') {
            steps {
                sh "./gradlew test"
            }
        }
	stage('build') {
            steps {
                sh "./gradlew build"
            }
        }
	stage('docker build') {
            steps {
                sh "sudo docker build -t localhost:5000/calculadora ."
            }
        }
	stage('docker push') {
            steps {
                sh "sudo docker push localhost:5000/calculadora"
            }
        }
	stage('docker delete container') {
	    when {
		expression { 
		    sh script: '''if [ -z $(sudo docker ps -a -f name=calculadora -q) ]; then true; else false; fi''', returnStatus: true
		}
	    }
            steps {
		sh "sudo docker stop calculadora"
                sh "sudo docker rm calculadora"
            }
        }
	stage('docker create container') {
            steps {
                sh "sudo docker run -d -p 9090:8090 --name calculadora localhost:5000/calculadora"
            }
        }
    }
}
