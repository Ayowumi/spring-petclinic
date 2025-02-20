pipeline {
    agent any
    triggers {
        cron('H/3 * * * 4') // Every 3 minutes on Thursdays
    }
    stages {
        stage('Build and Code Coverage') {
            steps {
                script {
                    // Clean and build the project, generate code coverage report
                    sh './gradlew clean build jacocoTestReport'
                }
            }
            post {
                success {
                    // Archive the artifact and the JaCoCo report
                    archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: false
                    publishHTML(target: [
                        reportName: 'JaCoCo Code Coverage',
                        reportDir: 'build/reports/jacoco/test/html',
                        reportFiles: 'index.html',
                        keepAll: true,
                        alwaysLinkToLastBuild: true
                    ])
                }
            }
        }
    }
}

