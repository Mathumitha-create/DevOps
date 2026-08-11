pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building HelloWeb...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh 'sudo cp target/*.war /opt/tomcat/webapps/'
                sh 'sudo systemctl restart tomcat'
            }
        }
    }

    post {
        success {
            echo 'HelloWeb deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}

