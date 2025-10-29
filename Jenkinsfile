pipeline {
    agent any
    environment {
        SONAR_HOME = tool "Sonar"
    }

    stages {
        stage('Code Clone') {
            steps {
                sh 'whoami'
                // Clone the repo manually instead of clone() syntax (Groovy doesn’t support that directly)
                git branch: 'main', url: 'https://github.com/ManishSingh-01/django-notes-app.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar') {
                    sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=my-project -Dsonar.projectKey=my-project"
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    // First stop any running containers
                    sh 'docker-compose down || true'

                    // Then rebuild and run in detached mode
                    sh 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline execution completed."
        }
    }
}


