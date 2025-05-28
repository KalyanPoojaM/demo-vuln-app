pipeline {
    agent any

    tools {
        maven 'Maven3' // Use the name you've configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/KalyanPoojaM/demo-vuln-app.git'
            }
        }

        stage('Run OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '',
                                odcInstallation: 'DependencyCheck', // Make sure this matches your Jenkins tool config
                                stopBuild: false
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
}
