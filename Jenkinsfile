pipeline {
    agent any

    stages {

        // stage('Code Quality Scan') {
        //     dir('./webgoat'){
        //         sh "mvn sonar:sonar -Dsonar.host.url=http://localhost:9000"
        //     }
        // }

        stage('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore clean package'
            }
            post {
                success {
                    echo 'Now archiving...'
                    archiveArtifacts artifacts: "**/target/*.war"
                }
            }
        }

        stage('Nexus IQ Scan'){
            steps {
                def policyEvaluation = nexusPolicyEvaluation failBuildOnNetworkError: false, iqApplication: 'webgoat-server-side', iqStage: 'build', jobCredentialsId: ''
                echo "====================================="
                echo 'IQ scan results'
                echo "-------------------------------------"
                sh 'echo ${policyEvaluation}'
                echo "====================================="
            }
        }    
    }
}


