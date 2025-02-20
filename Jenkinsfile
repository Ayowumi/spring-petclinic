pipeline {
    agent any
    triggers {
        cron('H/3 * * * 4') // Every 3 minutes on Thursdays
    }
    stages {
        stage('Build and Code Coverage') {
            steps {
                script {
                    // Clean, test, and generate code coverage report
                    sh './gradlew clean test jacocoTestReport'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'build/libs/*.jar', allowEmptyArchive: true
                    publishHTML(target: [
                        reportName : 'JaCoCo Report',
                        reportDir  : 'build/jacocoHtml',
                        reportFiles: 'index.html'
                    ])
                }
            }
        }
    }
}
