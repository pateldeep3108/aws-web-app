pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify WAR') {
            steps {
                sh 'test -f target/aws-web-app.war'
                sh 'ls -lh target/aws-web-app.war'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Maven WAR project built successfully!'
            archiveArtifacts artifacts: 'target/*.war',
                             fingerprint: true
        }

        failure {
            echo 'FAILED: Check the Jenkins console output.'
        }
    }
}
