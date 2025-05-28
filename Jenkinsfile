pipeline {
    agent any

    tools {
        // Install Maven if you're using it (optional)
        maven 'Maven 3.8.1'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/KalyanPoojaM/demo-vuln-app.git'
            }
        }

        stage('Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '', 
                    odcInstallation: 'Default', 
                    scanpath: '.', 
                    datadir: '', 
                    suppressionFile: '', 
                    outdir: 'dependency-check-report', 
                    isQuickMode: false, 
                    includeCsvReport: false, 
                    includeHtmlReport: true, 
                    includeJsonReport: true, 
                    includeJunitReport: false
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dependency-check-report/**', fingerprint: true
            publishHTML(target: [
                reportDir: 'dependency-check-report',
                reportFiles: 'dependency-check-report.html',
                reportName: 'OWASP Dependency-Check Report'
            ])
        }
    }
}
