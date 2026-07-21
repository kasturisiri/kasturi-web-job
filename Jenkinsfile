pipeline {
    agent any

    environment {
        PATH = "$PATH:/opt/apache-maven-3.6.3/bin"
    }

    stages {
        stage('GetCode') {
            steps {
                git(
                    url: 'https://github.com/kasturisiri/kasturi-web-job.git',
                    branch: 'main'
                )
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar-Server-9.9.8') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Code Deploy') {
            steps {
                sshagent(['Tomcat-Server-Agent']) {
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@http://34.227.224.202:9090:/home/ec2-user/apache-tomcat-9.0.63/webapps'
                }
            }
        }
    }
}
