pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t robot-demo .'
            }
        }

        stage('Run Robot Tests') {
            steps {
                bat 'docker rm -f robot-container || exit 0'
                bat 'docker run --name robot-container robot-demo'
            }
        }
    }

    post {
        always {
            bat 'docker cp robot-container:/app/output.xml .'
            bat 'docker cp robot-container:/app/log.html .'
            bat 'docker cp robot-container:/app/report.html .'

            robot outputPath: '.'
        }
    }
}
