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
                sh "docker build -t localhost:5000/calculadora"
            }
        }
	stage('docker push') {
            steps {
                sh "docker push localhost:5000/calculadora"
            }
        }
	stage('docker delete container') {
            steps {
                sh "docker rm calculadora"
            }
        }
	stage('docker create container') {
            steps {
                sh "docker run -d -p 9090:8090 --name calculadora localhost:5000/calculadora"
            }
        }
    }
}
