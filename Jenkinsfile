pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/KalyanPoojaM/demo-vuln-app.git'
            }
        }

        stage('Run OWASP Dependency Check') {
            steps {
                dependencyCheck odcInstallation: 'Default', additionalArguments: ''
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML(target: [
                    allowMissing: true,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'dependency-check-report',
                    reportFiles: 'dependency-check-report.html',
                    reportName: 'OWASP Dependency Check Report'
                ])
            }
        }
    }

    post {
        always {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
