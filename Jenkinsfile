pipeline {
    agent { label 'docker1' }

    stages {
        stage('buld test package') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean package'
            }
        }
        stage('test ssh remote execution') {
            steps {
                sshagent(credentials:['docker-worker-key']) {
                    // some block
                    sh "ssh -o StrictHostKeyChecking=no -l ubuntu 172.31.93.15 'whoami'"
                    sh "scp target/maven-web-application.war ubuntu@172.31.93.15:/opt/tomcat/webapps"
                }
            }
        }
    }
}