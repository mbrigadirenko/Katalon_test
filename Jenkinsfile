pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-repo/katalon-project.git'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'katalon-studio.sh --args "-runMode=console -projectPath="${WORKSPACE}" -browser="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/Your_Test_Suite"'
            }
        }

        stage('Generate Report') {
            steps {
                script {
                    katalon_reports = findFiles(glob: '**/katalon-report/**/*')
                    if (katalon_reports) {
                        publishHTML(target: [
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: katalon_reports[0].path,
                            reportFiles: 'index.html',
                            reportName: 'Katalon Test Report'
                        ])
                    }
                }
            }
        }
    }
}