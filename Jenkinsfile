pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                scp target/*.war ec2-user@<TOMCAT_SERVER_IP>:/opt/tomcat/webapps/
                ssh ec2-user@<TOMCAT_SERVER_IP> "sudo systemctl restart tomcat"
                '''
            }
        }
    }
}
