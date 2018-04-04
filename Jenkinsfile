pipeline {
    agent any

    stages {
        stage {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now archiving...'
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }
    }
}
