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

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar-Server-9.9.8') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
