
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm ci'
                bat 'npx playwright install chromium'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
    }

    post {
        always {
            // Publish the interactive Allure report
            allure([
                results: [[path: 'allure-results']]
            ])

            // Archive test reports
            archiveArtifacts(
                artifacts: 'playwright-report/**,allure-results/**',
                allowEmptyArchive: true
            )
        }
    }
}
