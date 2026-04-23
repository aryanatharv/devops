pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                bat '"C:\\Users\\Aryan Atharv\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" -m pip install pytest --quiet'
            }
        }

        stage('Run Tests') {
            steps {
                bat '"C:\\Users\\Aryan Atharv\\AppData\\Local\\Programs\\Python\\Python314\\python.exe" -m pytest -v --junitxml=results.xml'
            }
        }
    }

    post {
        always {
            junit 'results.xml'
        }

        success {
            emailext(
                to: 'aryanatharv03@gmail.com',
                subject: " BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h2>Build Successful</h2>
                <p><b>Job:</b> ${env.JOB_NAME}</p>
                <p><b>Build:</b> ${env.BUILD_NUMBER}</p>
                <p><a href="${env.BUILD_URL}">View Build</a></p>
                """,
                mimeType: 'text/html'
            )
        }

        failure {
            emailext(
                to: 'aryanatharv03@gmail.com',
                subject: " BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                <h2>Build Failed</h2>
                <p><b>Job:</b> ${env.JOB_NAME}</p>
                <p><b>Build:</b> ${env.BUILD_NUMBER}</p>
                <p><a href="${env.BUILD_URL}console">View Logs</a></p>
                """,
                mimeType: 'text/html'
            )
        }
    }
}
